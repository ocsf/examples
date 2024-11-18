# OCSF MITRE Intermediate Log Format (ILF) Encoding

For real-time analysis of cyber events, it is necessary to process event records from an event stream as quickly as possible to facilitate detection of adversary actions. Some techniques for speeding up the detection are partial interpretation of an event record, and applying regex to the event stream. MITRE developed Intermediate Log Format (ILF) format to enable such techniques. 



## ILF Record Structure

1. An ILF record (referred to simply as as “record” below) MUST have the following structure.
```
<event type>[<sender>,<receiver>,<time stamp>,(<attribute_fields>)] 
```
2. Every record ends with a space, inserted after the closing square brace “]”. Additional whitespace, such as newlines, can also follow the space.
3. The `<event type>`, `<sender>`, and `<receiver>` fields are interpreted as strings, and are not required to be in quotes.
    - An `<event type>` MUST consist of only alphanumeric characters or “_”.
    - The `<sender>` and `<receiver>` fields can contain alphanumeric characters or the characters ‘.’, ‘*’and ‘_’. The dot (.) character is used to specify hierarchy of components of the sender or receiver, e.g., car.brake.
    - The `<time stamp>` field MUST be compliant to these standards: ISO8601 or UNIX epoc. All `<time stamp>` fields in a stream of records must follow the same standard. The timestamp field can be empty. 
4. The fields, `<sender>`, `<receiver>`, and `<time stamp>`, are located at the first, second, and third locations, respectively, and are mandatory. 
    - These fields can be empty. 
    - If the `<sender>` or `<receiver>` values are not known or are irrelevant, their values can be *. 
    - If the record is broadcast, then the `<receiver>` field is *.
5. The fourth and last field of an ILF record, `<attribute_fields>`, contains semicolon-separated key-value pairs with the structure `<attribute_name>=<attribute_value>`
    - `<attribute fields>` can be empty, though the enclosing parentheses must remain.
    - An attribute name may contain alphanumeric characters, “.”, or “_”
    - `<attribute_value>` can be empty in some records in an event stream, as long as `<attribute_name>` is specified.
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
        - Dictionaries are sequences of key value pairs matched with semicolons, separated by commas, surrounded with curly brackets (e.g. {“key”: 4, “key2”:6.1 , “8”:677 }).
        - Keys in dictionaries MUST be strings.
        - The types of values in dictionaries can only be Strings or Numbers.
        - Whitespace is allowed around the keys or values.
    - Time
        - Specified based on the ISO8601 standard.
    - Enums
        - If a value can’t be parsed into one of the above forms, it is parsed as an enum. 
        - Enums can only contain alphanumeric characters, or ‘_’ and '.’.


## OCSF Event Type Mapping

OCSF supports several event classes and type IDs within each event classes. Mapping 

```
`Class__Activity` can be used for event type. For example `type_uid`:

The event/finding type ID. It identifies the event's semantics and structure. The value is calculated by the logging system as: `class_uid * 100 + activity_id`.

- **100400** Memory Activity: Unknown
- **100401** Memory Activity: Allocate Page
- **100402** Memory Activity: Modify Page
```

## Semantic Type Considerations

### Type Mappings

```markdown
## Rules for Flattening an OCSF Struct to an ILF

**Notes:**
- This process is recursive and builds a “path” for each entry as it deconstructs each value.
- “Special fields” are always ignored.

For each field in the OCSF:

1. **If it is a List/Vector:**
   - Add each element of the array, adding the index of the array entry to the path.

2. **If it is a Message:**
   - If it is `None`, add a `None` value to the ILF.
   - If it is not `None`, add each field in the Message according to these rules, adding the name of the field to the path.

3. **If it is an Enum:**
   - If it is `None`, add a `None` value to the ILF.
   - If it is not `None`, return the value of the Enum as an integer.

4. **If it is an Optional:**
   - If it is `None`, add a `None` value to the ILF.
   - If it is not `None`, add the value according to these rules.

5. **If it is a Protobuf Timestamp:**
   - Convert the timestamp to a RFC3339-compliant string and add the value to the ILF.

6. **If it is a Protobuf Generic Struct:**
   - Add each field in the Message according to these rules, adding the name of the field to the path.

7. **If it is a Protobuf Generic Value:**
   - If it is a List value, add the list according to the List rules.
   - If it is a Null or if it is a `None` value, add a `None` value to the ILF.
   - If it is a Struct value, add the struct according to the Struct rules.
   - If it is a Number value, add it as a Float value to the ILF.
   - If it is a String value, add it as a String value to the ILF.
   - If it is a Boolean value, add it as a Bool value to the ILF.

8. **If it is a String, Int, Float, Long, or Boolean:**
   - Add the value to the ILF.
```

Types not mentioned above are mapped to the protobuf type of their
underlying type.

TODO: figure out which types are using "underlying types".

### Structured Types

TODO: discuss struct and array unpacking
using JSON syntax (object.attribute)


