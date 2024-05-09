# OCSF Protobuf Encoding

This directory contains a sample Protobuf encoding for OCSF.

Although encoding in general is _informative_ in OCSF, enabling the
interoperation between systems in a single organization and indeed
between organizations indicates that a **canonical** protobuf encoding
has significant utility.  This directory contains that canonical
encoding.

## Semantic Type Considerations

### Primitive Types

The primitive types are mapped as follows

| OCSF Type   | Protobuf Type |
| ----------- | ------------- |
| `boolean_t` | `bool`        |
| `float_t`   | `float`       |
| `integer_t` | `int32`       |
| `long_t`    | `int64`       |
| `string_t`  | `string`      |
| `json_t`    | `bytes`       |

The mapping is straightforward, except to note that the bytes stored
in a `json_t` value should be the JSON-encoded version of the value.

For example, if in OCSF JSON you have:
```
{
  "class_uid": 3004,
  "entity": {
    "name": "admin policy",
    "data": {
      "gcp_policy_id": 82342521
    }
  },
  ...
}
```

then in protobuf you would have:
```
  class_uid: int32(3004)
  entity:
    name: string("admin policy")
    data: bytes("{\"gcp_policy_id\":82342521}")
  ...
```

### Other Types

Non-primitive types are mapped to the appropriate underlying
primitive type, with the following exceptions:

### Date Time

The `datetime_t` type is mapped to the timestamp object that comes
with protobuf, `google.protobuf.Timestamp`.

### Enumerated Values

Enumerated **integer** values are built using protobuf's `enum`
declaration.  Because OCSF often (not always) refines the set of
enumerands on a per-event basis, the protobuf encoding supports that
by making the enumeration types sub-names of the message types.
Furthermore, because Protobuf uses "C++" scoping rules, in which
enumerated values are in the same scope as the enum type itself
(rather than children of the type), we mangle the enumerand names as
well.

For example:
```
message FileActivity {
    enum ActionId {
        UNKNOWN_ActionId = 0;  // The action was unknown. The <code>disposition_id</code>
                               // attribute may still be set to a non-unknown value, for
                               // example 'Count', 'Uncorrected', 'Isolated',
                               // 'Quarantined' or 'Exonerated'.
        ALLOWED_ActionId = 1;  // The activity was allowed. The
                               // <code>disposition_id</code> attribute should be set to a
                               // value that conforms to this action, for example
                               // 'Allowed', 'Approved', 'Delayed', 'No Action', 'Count'
                               // etc.
        DENIED_ActionId  = 2;  // The attempted activity was denied. The
                               // <code>disposition_id</code> attribute should be set to a
                               // value that conforms to this action, for example
                               // 'Blocked', 'Rejected', 'Quarantined', 'Isolated',
                               // 'Dropped', 'Access Revoked, etc.
        OTHER_ActionId   = 99; // The action was not mapped. See the <code>action</code>
                               // attribute, which contains a data source specific value.
    }
    enum ActivityId {
        UNKNOWN_ActivityId        = 0; 
        CREATE_ActivityId         = 1;  // A request to create a new file on a file
                                        // system.
        READ_ActivityId           = 2;  // A request to read data from a file on a file
                                        // system.
        ...
    }
    ...
    ActionId action_id = 3;
    ActivityId activity_id = 4;
    ...
}
```

The protobuf encoding preserves the numerical value of the enumerand.
This is mostly for consistency with OCSF, but also helps with JSON
Encoding interoperability (see below).

However, not every enumeration in OCSF includes a 0 value, which is
required in proto3, so in cases where the 0 value is missing, an
`UNKNOWN` enumerand with the 0 value is inserted.

No special treatment is given for enumerated **string** values in
OCSF, they are just treated as strings by the protobuf encoding.

### Object and Event Types

Objects and Events are mapped to Protobuf `message` objects in the
straightforward way, preserving the OCSF name of the field (e.g.,
`status_id` instead of the more conventional Protobuf `statusId`)

The one exception is the unextended `object` in Protobuf is mapped
to a special message:

```
// generic object, e.g., for unmapped
message GenericObject {
   bytes jsonEncoded = 1;
}
```

The `jsonEncoded` holds the JSON encoded version of the object.
So, for example, if you have an OCSF JSON object like this:
```
{
  "class_uid": 3004,
  "unmapped": {
    "foo": 3,
    "bar": [1, 2]
  },
  ...
}
```

then that would be encoded in protobuf like so:
```
  class_uid: int32(3004)
  unmapped:
    jsonEncoded: bytes("{\"foo\":3,\"bar\":[1,2]}")
```

#### Field IDs

The Protobuf wire encoding requires consistent field ids for message
objects.  To facilitate interoperation and schema evolution, a
separate control file (the canonical version of which is included in
this repo in `control.json`) is used "remember" the field ids assigned
to fields in messages.

## Protobuf JSON Encoding

This encoding concerns itself primarily with the protobuf wire
representation.  Although protobuf defines a JSON encoding as well,
that JSON encoding always represents longs as strings (per the [I-JSON
recommendation](https://datatracker.ietf.org/doc/html/rfc7493#section-2.2))
so there is not direct interoperability between JSON-encoded protobof
and the OCSF JSON encoding.  However, despite that, this encoding
strives to preserve compability where possible (_i.e._, in field names)

In addition, by default the protobuf JSON encoding uses strings to
encode enumerations and converts to `lowerCamelCase` identifiers,
both of which are inconsistent with OCSF JSON encoding.

To obtain the closest representation of OCSF JSON, disable these
features.  In the protojson encoder for Go,
`google.golang.org/protobuf/encoding/protojson`, this can be
accomplished using non-default marshal options like so:

```
import "google.golang.org/protobuf/encoding/protojson"

func EncodeToJSON(item *proto.FileActivity) ([]byte, error) {

	// Note that the default behavior is to use strings for enums,
	// and to force lowerCamelCase, neither of which is what we
	// want for OCSF

	opt := protojson.MarshalOptions{
		UseEnumNumbers: true, // otherwise it will use strings
		UseProtoNames:  true, // otherwise it will try to force lowerCamelCase
	}
	return opt.Marshal(&item)
}
```
