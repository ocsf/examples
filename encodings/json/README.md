# OCSF JSON Encoding

Since OCSF was developed from a JSON perspective, there are not
a lot of things to call out here for best practices.

For example, the [OCSF server](https://github.com/ocsf/ocsf-server)
already contains tooling to export the schema in [JSON
Schema](https://json-schema.org/) format, which can be used
to automate validation of JSON-encoded OCSF events.

## Semantic Type Considerations

The `long_t` type in OCSF can be represented easily in JSON, but many
language processes of JSON (including Javascript itself) may not
handle the full range of values, since Javascript originally only had
a single numeric type, IEEE-754 double, which can only represent exact
integers up to to about 53 bits.

Furthemore, restricted profiles of JSON such as
[I-JSON](https://www.rfc-editor.org/rfc/rfc7493) specifically limit
the range of integers and the precision of floats and _recommend_ the
use of strings in cases where greater range or precision is required.

## Language Bindings

Language bindings are another matter.  Using the JSON schema to
generate language bindings loses a lot of semantics in translation;
for example, when using the **Date/Time** profile, OCSF includes an
[RFC-3339](https://www.rfc-editor.org/rfc/rfc3339.html) timestamp, for
which a JSON string regex constraint is defined.  However, most
languages would likely rather express a timestamp in their native time
representation (e.g., in Go a `time.Time` object) and leave it to the
language's JSON serdes to convert that back and forth to an RFC-3339
string in a JSON encoding.

## Concrete Type Mapping

For the JSON encoding, types are straightforwardly mapped and the
output of the server's JSON Schema is considered canonical for now.

### Object

Special consideration is given to the `object` type.  When it appears
_unextended_ as the type for an attribute in the schema (_e.g._, as it
does for the `unmapped` attribute on `BaseEvent`), then the
expectation is that it will be populated with properties not defined
by the schema.  In this sense it behaves similarly to `json_t`, except
that the former permits non-object values.

## Bundling

To support encoding multiple OCSF events into a single message, we
recommend a JSON-encoded _frame_ around multiple events.  This allows
additional properties to be included where that is helpful, and
supports easier future extensibility.

The frame should itself be a JSON object, and contain some properties:

| Property        | Requirement | Notes                                                       |
| --------------- | ----------- | ----------------------------------------------------------- |
| `events`        | required    | These are the actual events and the whole point of bundling |
| `start_time`    | optional    | The earliest timestamp_t of any bundled events              |
| `end_time`      | optional    | The latest timestamp_t of any bundled events                |
| `start_time_dt` | optional    | The earliest datetime_t of any bundled events               |
| `end_time_dt`   | optional    | The latest datetime_t of any bundled events                 |
| `count`         | optional    | The number of bundled events                                |

The `events` property is a just a JSON array of JSON-encoded OCSF
events.  It is the only required field, and is the whole point of
bundling.

Note that the bundle itself _is not_ an OCSF event.  In cases where
bundles and events may both be present, distinguishing between bundles
and OCSF events can be done either by inspecting the object and noting
the presence of lack of a `class_uid`, or by making use of out-of-band
metadata.

The rationale for using an array is that it is a simple JSON data type
to model a set of objects.  Despite the use of an array, it should be
noted that there is no intended ordering semantics of the events in
the bundle.

Some of the principal use cases considered include:

1. Bundling together multiple, unrelated events for transport in a
   batch to reduce transport overhead.
2. Bundling together related events, such as a detection finding
   being bundled together with some underlying events that led
   to the detection firing.

Here is a sketch of an example bundle:

```
{
    "start_time": 1713632701123,
    "start_time_dt": "2024-04-20T17:05:01.123456Z",
    "end_time": 1713634257679,
    "end_time_dt": "2024-04-20T17:30:57.678912304Z",
    "events": [
        {
            "class_uid": 5001,
            "type_uid": 500102,
            ... details about the discovery event ...
        },
        {
            "class_uid": 2002,
            "type_uid": 200201,
            ... details about the vuln finding event ...
        }
    ]
}
```
