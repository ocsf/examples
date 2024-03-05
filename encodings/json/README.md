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

