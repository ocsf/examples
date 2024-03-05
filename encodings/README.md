# OCSF Encodings

This repository contains information, recommendations, and tools to
support representations of events described by the OCSF abstract
schema.  Representations include both *encodings*, which are ways of
serializing OCSF events into sequences of bytes, and *in memory*
representations, which support managing OCSF events to native objects
within particular languages or systems.  (Some encodings, like
**protobuf** blur the distinction because they have a well defined
serialization but also their own ecosystem for creating language
representations based on the abstract protobuf description.)

## Organization of this Repository

This repository is organized by _representation_, so for example
information and tools to support JSON encodings are found in the
[`json/`](json/README.md) directory.

## Process for Developing an Encoding

This describes the general process to develop a new encoding.

### Use Cases

Identify and articulate the use cases that the encoding is intended to
target.  This will not only help guide choices in the encoding mapping
process, but also inform others as to when a particular encoding might
be useful to adopt.

### Primitive Data Types

Map the OCSF primitive data types to those available in the encoding.

The OCSF primitive types are the types in the dictionary
(`dictionary.json`, `types`) which do *not* have a `type` property.
This is the current list of all primitive types:

| Type        | Notes                            |
| ----------- | -------------------------------- |
| `boolean_t` | `true` or `false`                |
| `float_t`   | possibly non-integer number      |
| `integer_t` | smallish (~32 bit) integer       |
| `long_t`    | bigish (~64 bit) integer         |
| `string_t`  | a string of unicode characters   |
| `json_t`    | arbitrary JSON                   |

### Non-primitive scalar types

Determine the representation for non-primitive scalar types, which are
the types in the dictionary which *do* have a `type` property.

This is the current list as of `1.1.0`

| Type             | Primitive  | Notes                                      |
| --------------   | ---------- | ------------------------------------------ |
| `bytestring_t`   | `string_t` | base64 encoded bytes                       |
| `datetime_t`     | `string_t` | RFC-3339 timestamp                         |
| `email_t`        | `string_t` | Email address                              |
| `file_hash_t`    | `string_t` | Hash of file contents                      |
| `file_name_t`    | `string_t` | File name                                  |
| `hostname_t`     | `string_t` | Unique name for a network device           |
| `ip_t`           | `string_t` | IP address in IPv4 dotted notation or IPv6 |
| `mac_t`          | `string_t` | MAC address                                |
| `port_t`         | `integer_t`| TCP/UDP port number                        |
| `process_name_t` | `string_t` | Process name                               |
| `resource_uid_t` | `string_t` | Resource unique identifier                 |
| `subnet_t`       | `string_t` | Subnet in CIDR notation                    |
| `timestamp_t`    | `long_t`   | Epoch milliseconds                         |
| `url_t`          | `string_t` | URL                                        |
| `username_t`     | `string_t` | User name                                  |
| `uuid_t`         | `string_t` | 128-bit universal unique id (string repr)  |

Note that there are value constraints on many of these types.  In the
OCSF schema, these constraints are typically represented either by
`range` properties for numeric types, or `regex` and `max_len`
properties for string types.

An encoding MAY represent these types not as the indicated underlying
primitive type, but using another representation, provided that:

1. all *valid* values for the OCSF schema type in JSON can be
   represented in the encoding, AND
2. the mapping from JSON representation to the encoding is value
   preserving in both directions

For example, an encoding MAY represent `port_t` as a 16 bit unsigned
integer because the OCSF constraint is that it is an integer between 0
and 65535 inclusive.

As another example, a representation MAY encode `ip_t` using a native
language feature, provided that both IPv4 and IPv6 are representable,
as that is implied by the regex pattern used in the OCSF schema to
constrain the JSON encoding.

### Objects

TODO

#### Missing values

An encoding MUST preserve the semantics of missing values for non-required
fields.

For example, a naive encoding in protobuf does not distinguish between
0-valued integers and missing values.  Hence, if an attribute of type
`port_t` is optional, a naive encoding would not be permitted because
the encoding must distinguish between an attribute which is present
and has value `0` and an attribute which is not present.

### Classes

TODO

### Version Evolution

TODO

### Tooling

TODO

- tools to support transforming the OCSF schema, or a local extension
  thereof, into a machine-readable representation appropriate for the
  encoding and/or language binding
- tools or libraries to support translating or validating OCSF events
  (instances of classes)
  
