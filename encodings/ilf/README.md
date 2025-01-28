# OCSF MITRE Intermediate Log Format (ILF) Encoding

For real-time analysis of cyber events, it is necessary to process event records from an event stream as quickly as possible to facilitate detection of adversary actions. Some techniques for speeding up the detection are partial interpretation of an event record, and applying regex to the event stream. [MITRE](https://www.mitre.org/) developed Intermediate Log Format (ILF) format to enable such techniques. 

The scope of the mapping specified here is limited to one way translation from OCSF JSON records to ILF records. In the future, a reverse translation, from ILF records to OCSF may be contemplated.

We discuss some of the implementation considerations for an OCSF to ILF translation tool that implements the algorithms/rules described below in a [section below](#implementation-considerations).

## ILF Record Structure

1. An ILF record (referred to simply as as “record” below) MUST have the following structure.
```
<event type>[<sender>,<receiver>,<time stamp>,(<attribute fields>)] 
```
2. Every record ends with a space, inserted after the closing square brace “]”. Additional whitespace, such as newlines, can also follow the space.
3. The `<event type>`, `<sender>`, and `<receiver>` fields are interpreted as strings, and are not required to be in quotes.
    - An `<event type>` MUST consist of only alphanumeric characters or “_”.
    - The `<sender>` and `<receiver>` fields can contain alphanumeric characters and the characters ‘.’, ‘*’and ‘_’. The dot (`.`) character is used to specify hierarchy of components of the sender or receiver, e.g., car.brake
    - The `<time stamp>` field MUST be compliant to these standards: RFC 3339 or UNIX epoc. All `<time stamp>` fields in a stream of records must follow the same standard. The timestamp field can be empty. 
4. The fields, `<sender>`, `<receiver>`, and `<time stamp>`, are located at the first, second, and third locations, respectively. 
    - These fields may be empty, though the comma separators of the fields MUST be present. e.g., `OCSF_100400[,,,()] ` is a valid ILF record.
    - If the `<sender>` or `<receiver>` values are not known or are irrelevant, their values can be *. 
    - If the record is broadcast, then the `<receiver>` field is *.
5. The fourth and last field of an ILF record, `<attribute fields>`, contains semicolon-separated key-value pairs with the structure `<attribute_name>=<attribute_value>`
    - `<attribute fields>` can be empty, though the enclosing parentheses must remain.
    - An attribute name may contain alphanumeric characters, “.”, or “_”
    - `<attribute_value>` can be empty in some records in an event stream, as long as `<attribute_name>=` is specified. 
    - `<attribute_value>` is interpreted based on the event and component structure definitions provided to the ILF consumer.
    - When an `<attribute_value>` is a string, it is enclosed in double quotes, and the string content within the quotes must be escaped appropriately and conform to Java string escape conventions.
    - The key-value pairs need not follow the same location order in different ILF records in the same event stream.
6. The values of the attributes in the fourth field can be a String, Number, Array, Dictionary, or Time, as defined below.
    - Strings
        - Strings may be enclosed in single quotes or double quotes.
        - Strings may be encoded as UTF-8, UTF-16, or UTF-32 characters, depending on what the ILF consumer expects.
        - All other character escapes are ignored by the ILF consumer and passed through. (e.g. \n is kept as \n, not turned into a newline.)
    - Numbers
        - Integer, long, double, including signed prefixes (e.g., 2.1, -17, -17.0, 17l). 
        - Base-10 float, including signed exponents (e.g., 10.3e-3). 
        - Binary numbers are prefixed with 0b (e.g., 0b1100).
        - Octal numbers are prefixed with 0o (e.g., 0o723).
        - Hex numbers are prefixed with 0x (e.g., 0x93ABCDEF).
    - Arrays
        - Arrays are sequences of numbers, separated by commas, surrounded with square brackets (e.g., [1,0, 45, 6 ], [0x93AB,0x1F] ).
        - Only Numbers and Strings are allowed in arrays.
        - Whitespace is allowed around the array values.
    - Dictionaries
        - Dictionaries are sequences of key value pairs matched with colons, separated by commas, surrounded with curly brackets (e.g. {“key”: 4, “key2”:6.1 , “8”:677 }).
        - Keys in dictionaries MUST be strings.
        - The types of values in dictionaries can only be Strings or Numbers.
        - Whitespace is allowed around the keys or values.
    - Time
        - Specified based on the RFC 3339 or Unix epoc standard. 
    - Enums
        - Enums can only contain alphanumeric characters, or ‘_’ and '.’.
          
If the value of an attribute cannot be parsed as a String, Number, Array, Dictionary, or Time, an attempt will be made to parse it as an enum. A failure to parse may be flagged an error, or ignored.

## OCSF to ILF Event Type Mapping

OCSF supports several event classes and type IDs within each event classes. The ILF event_type is the same as OCSF `type ID`, calculated  as: OCSF_`Class UID * 100 + Activity ID`.  Below are some examples.

| OCSF Class UID: Name              | OCSF Activity ID :Name             |       ILF Event Type|
| ------------ | --------------------------- | --------- |
| `1004: Memory Activity`| `0` : Unknown| `OCSF_100400` |
| `1004: Memory Activity`| `1` : Allocate Page| `OCSF_100401` |
| `1004: Memory Activity`| `2`:  Modify Page| `OCSF_100402` |


## ILF Sender and Receiver Fields Mapping

ILF sender field will be, by default, the `metadata.product.name` field of an OCSF event record. This default can be changed in the ILF using the `_` to concatenate the multiple fields, e.g., changed to the concatenated `product.name` and `product.version` fields of OCSF Metadata object with with a `_`. A specific example of such a concatenation is:  `AWS_audit_d_k8s_d_io_fs_v1`, corresponding  to the product name field of `AWS` and product version of `audit.k8s.io/v1`.

The nonalphanumeric characters in the contributing fields to the ILF  `sender` field of ILF will be replaced based on the rules described below in [section](#ilf-attribute-names).

When translated from an OCSF record, the receiver field in an ILF record will always be `*`.
 
## ILF Timestamp
ILF time stamp will be the time when the ILF record is created. The other time mesurements are available as attribute fields in ILF, if necessary.

## OCSF to ILF Attribute Fields Mapping

Special fields in OCSF such as unmapped data may be excluded from the resulting ILF record.
Unlike formats such as JSON, ILF does not allow nested data objects or structs when transporting data, which implies that when translating an OCSF object, we need to "flatten" the object and all it's nested fields into a one-dimensional array of keys and values. We do this via the recursive process below:

### Process for Flattening an OCSF object as ILF Attribute Field Key Value Pair(s)

Start with an empty list of Key, Value pairs and an empty "Path". The Path acts as the attribute Key in the ILF record, and describes the hierarchy of where the data is located in the OCSF record.

For a given OCSF Message Element D:

1. If the type of D is an Object field or Unmapped Dictionary:
    - If the value of D is not `null`, for each field in the Object or Dictionary, flatten the value of the field with the field's name or key added to the path. Add all flattened fields to the ILF's list of Key, Value pairs.
      - e.g. for the nested data `{"hello": {"world": 1}}` the resulting flattened key, value pair would be `(hello_d_world, 1)`
    - If the value of D is `null`,  add a `null` value at the current Path to the ILF's list of Key, Value pairs.
      - e.g. for the nested data `{"hello": null}` the resulting flattened key, value pair would be `(hello, null)`
2. If the type of D is a List or Vector
    - For each entry in the List, flatten the entry with the entry's index in the List added to the path. Add all flattened entries to the ILF's list of Key, Value pairs.
      - e.g. for the nested data `{"hello": [1,2]}` the resulting flattened key, value pairs would be `(hello_d_0, 1), (hello_d_1, 2)`
3. If the type of D is an Enum
    - If the value of D is not `null`, add the path of the enum and the value of the Enum as an integer to the ILF's list of Key, Value pairs
    - If the value of D is `null`,  add a `null` value at the current Path to the ILF's list of Key, Value pairs.
4. If the type of D is a Timestamp
    - Convert the timestamp to a RFC3339-compliant string and add the path of the timestamp and the RFC3339-Compliant String to the ILF's list of Key, Value pairs.
      - e.g. for the data `{"start_time_dt": "2021-09-07T20:37:30.502680Z"}` the resulting flattened Key, Value pairs would be `("start_time_dt", "2021-09-07T20:37:30.502680+00:00")`
      - Note that we use RFC3339 timestamp here to align with other OCSF encodings
5. If the type of D is a basic Value (String, Boolean, Integer, Long, or Float)
    - Add it's path and Value to the ILF's list of Key, Value pairs.
      - e.g. for the data `{"data": {"int": 1, "bool": true, "float": 0.12, "null": null}}` the resulting flattened Key, Value pairs would be `[(data.int, 1), (data.bool, true), (data.float, 0.12), (data.null, "null")]`

At the end of this process, we should have a list of Key, Value pairs that encompass all the structured data from the OCSF object which we use as the ILF's attribute fields.

### ILF Attribute Names 

Some ILF receivers, i.e., tools that process the ILF formatted event records, may not be able to correctly process some of the non-alphanueric characters in the attribute names, except `_`. In such cases,  the  conversion table below will be used to translate such characters. Characters not in this table are disallowed entirely and cannot be mapped to ILF event records. An OCSF to ILF translator may not do such translation if the receiver can process the original characters correctly.

If the OCSF names do have any of these replacement strings in it, an extra `_` will be added before and after that replacement string, e.g., `xyz_d_abc` will be replaced by `xyz__d__abc`. This is done to support a future reverse mapping from ILF events to OCSF event.

| Character | Replacement String |
| --------- | ------------------ |
| `!` | `_ex_` |
| `@` | `_at_` |
| `#` | `_ot_` |
| `$` | `_dl_` |
| `%` | `_pc_` |
| `^` | `_ct_` |
| `&` | `_am_` |
| `*` | `_st_` |
| `(` | `_op_` |
| `)` | `_cp_` |
| `{` | `_ob_` |
| `}` | `_cb_` |
| `[` | `_os_` |
| `]` | `_cs_` |
| `:` | `_co_` |
| `"` | `_dq_` |
| `;` | `_sc_` |
| `'` | `_sq_` |
| `<` | `_lt_` |
| `>` | `_gt_` |
| `,` | `_co_` |
| `.` | `_d_` |
| `` ` `` | `_bt_` |
| `~` | `_ti_` |
| `-` | `_mi_` |
| `+` | `_pu_` |
| `=` | `_eq_` |
| `/` | `_fs_` |
| `?` | `_qm_` |
| `\|` | `_pi_` |
| `\` | `_bs_` |


### Types used in ILF encoding

The ILF encoding types are based on the Protobuf types. Special cases are made for Values of type null_value, struct_value, and list_value- these are "flattened" as described in the process above.

We also include below the types used in the Rust implementation of the OCSF to ILF universal translator.

| OCSF Type    | Protobuf Type               | ILF Type  | Rust Type |
| ------------ | --------------------------- | --------- | --------- |
| `boolean_t`  | `bool`                      | `bool`    | `bool` | 
| `float_t`    | `double`                    | `double`  |`f32` |
| `integer_t`  | `int32`                     | `integer` | `i32` | 
| `long_t`     | `int64`                     | `long`    | `i64` |
| `string_t`   | `string`                    | `string`  | `String` |
| `datetime_t` | `google.protobuf.Timestamp` | `string`  | `String` (Encoded with RFC3339) |
| `json_t`     | `google.protobuf.Value`     | see below for types based on variants of the Value type |

| `google.protobuf.Value` Variant |ILF Type | Rust type | 
| --------------------------------| -------- |--------- |
| number_value                    | `double`   | `f32`    |
| string_value                    | `string`   |`String` |
| bool_value                      | `bool`   | `bool`   |
| null_value                      | `null`   | `None`   |
| struct_value                    | [See above](#process-for-flattening-an-ocsf-object-as-ilf-attribute-field-key-value-pairs) |flattened set of Key, Value pairs |
| list_value                      |[See above](#process-for-flattening-an-ocsf-object-as-ilf-attribute-field-key-value-pairs)| flattened set of Key, Value pairs | 

## Implementation Considerations

For ILF, reducing the size of the event record is an important consideration. An OCSF to ILF translator has the option of improvements based on the following possibilities.

1. A prototype that translates OCSF events to ILF events is at [OCSF-to-ILF-translator](https://github.com/mitre/ocsf_ilf_translator)
2. A processor of ILF records may assume that the types of the ILF `<time stamp>` field and the attributes are known and available. An OCSF to ILF translator may provide this information to an ILF processor.
3. OCSF does not distinguish between a missing field in an event vs. the value of the field being null. ILF does make this distinction, and an ILF translator could potentially flag missing fields. However, the OCSF to ILF translation will ignore such missing fields in an incoming OCSF event. 
4. The `unmapped` objects and fields may be optionally not included in the ILF record.
5. The mapping of nonalphanumeric characters [above](#ilf-attribute-names) may be configured to use the original character, e.g., `.` instead of `_d_`, if the receiver of the ILF events can correctly process them.
6. The `sender` may be changed as described [above](#ilf-sender-and-receiver-fields-mapping).

## Example Mappings from an OCSF JSON to ILF

The examples are in the directory [example_logs](./example_logs)

