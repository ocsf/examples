# OCSF MITRE Intermediate Log Format (ILF) Encoding

For real-time analysis of cyber events, it is necessary to process event records from an event stream as quickly as possible to facilitate detection of adversary actions. Some techniques for speeding up the detection are partial interpretation of an event record, and applying regex to the event stream. MITRE developed Intermediate Log Format (ILF) format to enable such techniques. 

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
    - The `<sender>` and `<receiver>` fields can contain alphanumeric characters or the characters ‘.’, ‘*’and ‘_’. The dot (`.`) character is used to specify hierarchy of components of the sender or receiver, e.g., car.brake
    - The `<time stamp>` field MUST be compliant to these standards: ISO8601 or UNIX epoc. All `<time stamp>` fields in a stream of records must follow the same standard. The timestamp field can be empty. Exception - though ISO8601 permits both comma (`,`) and dot (`.`) for decimal points, in ILF, only dot (`.`) must be used to demote decimal points.
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
        - Integer, long, double, including signed prefixes (e.g., 2.1, -17, -17.0, 17l). Exception - though ISO8601 permits both comma (`,`) and dot (`.`) for decimal points, in ILF, only dot (`.`) must be used as decimal points.
        - Base-10 float, including signed exponents (e.g., 10.3e-3). Exception - though ISO8601 permits both comma (`,`) and dot (`.`) for decimal points, in ILF, only dot (`.`) must be used as decimal points.
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
        - Specified based on the ISO8601 standard. Exception - though ISO8601 permits both comma (`,`) and dot (`.`) for decimal points, in ILF, only dot (`.`) must be used as decimal points.
    - Enums
        - If a value can’t be parsed into one of the above forms, it is parsed as an enum. 
        - Enums can only contain alphanumeric characters, or ‘_’ and '.’.


## OCSF to ILF Event Type Mapping

OCSF supports several event classes and type IDs within each event classes. The ILF event_type is the same as OCSF `type ID', calculated  as: OCSF_`Class UID * 100 + Activity ID`.  Below are some examples.

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

OCSF events do not distinguish between a missing field or a field with a NULL value, whereas ILF does. Therefore, if a field is missing in the OCSF JSON, ILF provides the option to either produce an attribute field key with NULL value, or to remove the attribute key entirely from the JSON. Additionally, Special fields such as unmapped data may be excluded from the resulting ILF record.

Unlike formats such as JSON, ILF does not allow nested data objects or structs when transporting data- this means that when translating an OCSF object, we need to "flatten" the object and all it's nested fields into a one-dimensional array of keys and values. We do this via the recursive process below:

### Process for Flattening an OCSF object as ILF Attribute Field Key Value Pair(s)

Start with an empty list of Key, Value pairs and an empty "Path". The Path acts as the attribute Key in the ILF record, and describes the hierarchy of where the data is located in the OCSF record.

For a given OCSF Message Element D:

1. If the type of D is an Object field or Unmapped Dictionary:
    - If D the value of is not None, for each field in the Object or Dictionary, flatten the value of the field with the field's name or key added to the path. Add all flattened fields to the ILF's list of Key, Value pairs.
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
5. If the type of D is a basic Value (String, Boolean, Integer, Long, Float, or Null)
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

1. The `unmapped` objects and fields may be optionally not included in the ILF record. 
2. Since ILF does differentiate between the existence of an attribute vs. the attribute value being NULL, the ILF translator may optionally remove the attributes from ILF records, if the value of the incoming OCSF object or field is NULL or not present.
3. The mapping of nonalphanumeric characters [above](#ilf-attribute-names) may be configured to use the original character, e.g., `.` instead of `_d_`, if the receiver of the ILF events can correctly process them.
4. The `sender` may be changed as described [above](#ilf-sender-and-receiver-fields-mapping).

## Example Mapping from an OCSF JSON to ILF

Sample OCSF record (ocsf_eks.json)

```
{
    "activity_id": 1,
    "activity_name": "Create",
    "actor": {
      "session": {
        "credential_uid": "EXAMPLEUIDTEST",
        "issuer": "arn:aws:iam::123456789012:role/example-test-161366663-NodeInstanceRole-abc12345678912",
        "uid": "i-12345678901"
      },
      "user": {
        "groups": [
          {
            "name": "system:bootstrappers"
          },
          {
            "name": "system:nodes"
          },
          {
            "name": "system:authenticated"
          }
        ],
        "name": "system:node:ip-192-001-02-03.ec2.internal",
        "type_id": 0,
        "uid": "heptio-authenticator-aws:123456789012:ABCD1234567890EXAMPLE"
      }
    },
    "api": {
      "operation": "create",
      "request": {
        "uid": "f47c68f2-d3ac-4f96-b2f4-5d497bf79b64"
      },
      "response": {
        "code": 201
      },
      "version": "v1"
    },
    "category_name": "Application Activity",
    "category_uid": 6,
    "class_name": "API Activity",
    "class_uid": 6003,
    "cloud": {
      "account": {
        "uid": "arn:aws:sts::123456789012:assumed-role/example-test-161366663-NodeInstanceRole-abc12345678912/i-12345678901"
      },
      "provider": "AWS"
    },
    "http_request": {
      "url": {
        "path": "/api/v1/nodes"
      },
      "user_agent": "kubelet/v1.21.2 (linux/amd64) kubernetes/729bdfc"
    },
    "message": "ResponseComplete",
    "metadata": {
      "log_level": "RequestResponse",
      "product": {
        "feature": {
          "name": "Elastic Kubernetes Service"
        },
        "name": "Amazon EKS",
        "vendor_name": "AWS",
        "version": "audit.k8s.io/v1"
      },
      "profiles": [
        "cloud",
        "datetime"
      ],
      "version": "1.2.0"
    },
    "observables": [
      {
        "name": "actor.user.name",
        "type": "User Name",
        "type_id": 4,
        "value": "system:node:ip-192-001-02-03.ec2.internal"
      },
      {
        "name": "src_endpoint.ip",
        "type": "IP Address",
        "type_id": 2,
        "value": "12.000.22.33"
      },
      {
        "name": "http_request.url.path",
        "type": "URL String",
        "type_id": 6,
        "value": "/api/v1/nodes"
      }
    ],
    "resources": [
      {
        "name": "ip-192-001-02-03.ec2.internal",
        "namespace": null,
        "type": "nodes",
        "uid": null,
        "version": null
      }
    ],
    "severity": "Informational",
    "severity_id": 1,
    "src_endpoint": {
      "ip": "12.000.22.33"
    },
    "start_time": 1631047050502680,
    "start_time_dt": "2021-09-07T20:37:30.502680Z",
    "time": 1631047050642854,
    "time_dt": "2021-09-07T20:37:30.642854Z",
    "type_name": "API Activity: Create",
    "type_uid": 600301,
    "unmapped": {
      "annotations": {
        "authorization.k8s.io/decision": "allow",
        "authorization.k8s.io/reason": ""
      },
      "kind": "Event",
      "objectRef": {},
      "requestObject": {
        "apiVersion": "v1",
        "kind": "Node",
        "metadata": {
          "annotations": {
            "volumes.kubernetes.io/controller-managed-attach-detach": "true"
          },
          "creationTimestamp": null,
          "labels": {
            "alpha.eksctl.io/cluster-name": "ABCD1234567890EXAMPLE",
            "alpha.eksctl.io/nodegroup-name": "ng-5fe434eb",
            "beta.kubernetes.io/arch": "amd64",
            "beta.kubernetes.io/instance-type": "m5.xlarge",
            "beta.kubernetes.io/os": "linux",
            "eks.amazonaws.com/capacityType": "ON_DEMAND",
            "eks.amazonaws.com/nodegroup": "ng-5fe434eb",
            "eks.amazonaws.com/nodegroup-image": "ami-0193ebf9573ebc9f7",
            "eks.amazonaws.com/sourceLaunchTemplateId": "lt-0f20d6f901007611e",
            "eks.amazonaws.com/sourceLaunchTemplateVersion": "1",
            "failure-domain.beta.kubernetes.io/region": "us-east-1",
            "failure-domain.beta.kubernetes.io/zone": "us-east-1f",
            "kubernetes.io/arch": "amd64",
            "kubernetes.io/hostname": "ip-192-001-02-03.ec2.internal",
            "kubernetes.io/os": "linux",
            "node.kubernetes.io/instance-type": "m5.xlarge",
            "topology.kubernetes.io/region": "us-east-1",
            "topology.kubernetes.io/zone": "us-east-1f"
          },
          "name": "ip-192-001-02-03.ec2.internal"
        },
        "spec": {
          "providerID": "aws:///us-east-1f/i-12345678901"
        },
        "status": {
          "addresses": [
            {
              "address": "192.000.22.33",
              "type": "InternalIP"
            },
            {
              "address": "12.000.22.33",
              "type": "ExternalIP"
            },
            {
              "address": "ip-192-001-02-03.ec2.internal",
              "type": "Hostname"
            },
            {
              "address": "ip-192-001-02-03.ec2.internal",
              "type": "InternalDNS"
            },
            {
              "address": "ec2-12.000.22.33.compute-1.amazonaws.com",
              "type": "ExternalDNS"
            }
          ],
          "allocatable": {
            "attachable-volumes-aws-ebs": "25",
            "cpu": "3920m",
            "hugepages-1Gi": "0",
            "hugepages-2Mi": "0",
            "memory": "15076868Ki",
            "pods": "58"
          },
          "capacity": {
            "attachable-volumes-aws-ebs": "25",
            "cpu": "4",
            "hugepages-1Gi": "0",
            "hugepages-2Mi": "0",
            "memory": "16093700Ki",
            "pods": "58"
          },
          "conditions": [
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "kubelet has sufficient memory available",
              "reason": "KubeletHasSufficientMemory",
              "status": "False",
              "type": "MemoryPressure"
            },
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "kubelet has no disk pressure",
              "reason": "KubeletHasNoDiskPressure",
              "status": "False",
              "type": "DiskPressure"
            },
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "kubelet has sufficient PID available",
              "reason": "KubeletHasSufficientPID",
              "status": "False",
              "type": "PIDPressure"
            },
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "[container runtime status check may not have completed yet, container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized, CSINode is not yet initialized, missing node capacity for resources: ephemeral-storage]",
              "reason": "KubeletNotReady",
              "status": "False",
              "type": "Ready"
            }
          ],
          "daemonEndpoints": {
            "kubeletEndpoint": {
              "Port": 10250
            }
          },
          "nodeInfo": {
            "architecture": "amd64",
            "bootID": "0d0dd4f2-8829-4b03-9f29-794f4908281b",
            "containerRuntimeVersion": "docker://19.3.13",
            "kernelVersion": "5.4.141-67.229.amzn2.x86_64",
            "kubeProxyVersion": "v1.21.2-eks-55daa9d",
            "kubeletVersion": "v1.21.2-eks-55daa9d",
            "machineID": "ec2483c633b0e271f36ce14e45a361b8",
            "operatingSystem": "linux",
            "osImage": "Amazon Linux 2",
            "systemUUID": "ec2483c6-33b0-e271-f36c-e14e45a361b8"
          }
        }
      },
      "responseObject": {
        "apiVersion": "v1",
        "kind": "Node",
        "metadata": {
          "annotations": {
            "volumes.kubernetes.io/controller-managed-attach-detach": "true"
          },
          "creationTimestamp": "2021-09-07T20:37:30Z",
          "labels": {
            "alpha.eksctl.io/cluster-name": "ABCD1234567890EXAMPLE",
            "alpha.eksctl.io/nodegroup-name": "ng-5fe434eb",
            "beta.kubernetes.io/arch": "amd64",
            "beta.kubernetes.io/instance-type": "m5.xlarge",
            "beta.kubernetes.io/os": "linux",
            "eks.amazonaws.com/capacityType": "ON_DEMAND",
            "eks.amazonaws.com/nodegroup": "ng-5fe434eb",
            "eks.amazonaws.com/nodegroup-image": "ami-0193ebf9573ebc9f7",
            "eks.amazonaws.com/sourceLaunchTemplateId": "lt-0f20d6f901007611e",
            "eks.amazonaws.com/sourceLaunchTemplateVersion": "1",
            "failure-domain.beta.kubernetes.io/region": "us-east-1",
            "failure-domain.beta.kubernetes.io/zone": "us-east-1f",
            "kubernetes.io/arch": "amd64",
            "kubernetes.io/hostname": "ip-192-001-02-03.ec2.internal",
            "kubernetes.io/os": "linux",
            "node.kubernetes.io/instance-type": "m5.xlarge",
            "topology.kubernetes.io/region": "us-east-1",
            "topology.kubernetes.io/zone": "us-east-1f"
          },
          "managedFields": [
            {
              "apiVersion": "v1",
              "fieldsType": "FieldsV1",
              "fieldsV1": {
                "f:metadata": {
                  "f:annotations": {
                    ".": {},
                    "f:volumes.kubernetes.io/controller-managed-attach-detach": {}
                  },
                  "f:labels": {
                    ".": {},
                    "f:alpha.eksctl.io/cluster-name": {},
                    "f:alpha.eksctl.io/nodegroup-name": {},
                    "f:beta.kubernetes.io/arch": {},
                    "f:beta.kubernetes.io/instance-type": {},
                    "f:beta.kubernetes.io/os": {},
                    "f:eks.amazonaws.com/capacityType": {},
                    "f:eks.amazonaws.com/nodegroup": {},
                    "f:eks.amazonaws.com/nodegroup-image": {},
                    "f:eks.amazonaws.com/sourceLaunchTemplateId": {},
                    "f:eks.amazonaws.com/sourceLaunchTemplateVersion": {},
                    "f:failure-domain.beta.kubernetes.io/region": {},
                    "f:failure-domain.beta.kubernetes.io/zone": {},
                    "f:kubernetes.io/arch": {},
                    "f:kubernetes.io/hostname": {},
                    "f:kubernetes.io/os": {},
                    "f:node.kubernetes.io/instance-type": {},
                    "f:topology.kubernetes.io/region": {},
                    "f:topology.kubernetes.io/zone": {}
                  }
                },
                "f:spec": {
                  "f:providerID": {}
                }
              },
              "manager": "kubelet",
              "operation": "Update",
              "time": "2021-09-07T20:37:30Z"
            }
          ],
          "name": "ip-192-001-02-03.ec2.internal",
          "resourceVersion": "67933403",
          "uid": "4ecf628a-1b50-47ed-932c-bb1df89dad10"
        },
        "spec": {
          "providerID": "aws:///us-east-1f/i-12345678901",
          "taints": [
            {
              "effect": "NoSchedule",
              "key": "node.kubernetes.io/not-ready"
            }
          ]
        },
        "status": {
          "addresses": [
            {
              "address": "192.000.22.33",
              "type": "InternalIP"
            },
            {
              "address": "12.000.22.33",
              "type": "ExternalIP"
            },
            {
              "address": "ip-192-001-02-03.ec2.internal",
              "type": "Hostname"
            },
            {
              "address": "ip-192-001-02-03.ec2.internal",
              "type": "InternalDNS"
            },
            {
              "address": "ec2-12.000.22.33.compute-1.amazonaws.com",
              "type": "ExternalDNS"
            }
          ],
          "allocatable": {
            "attachable-volumes-aws-ebs": "25",
            "cpu": "3920m",
            "hugepages-1Gi": "0",
            "hugepages-2Mi": "0",
            "memory": "15076868Ki",
            "pods": "58"
          },
          "capacity": {
            "attachable-volumes-aws-ebs": "25",
            "cpu": "4",
            "hugepages-1Gi": "0",
            "hugepages-2Mi": "0",
            "memory": "16093700Ki",
            "pods": "58"
          },
          "conditions": [
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "kubelet has sufficient memory available",
              "reason": "KubeletHasSufficientMemory",
              "status": "False",
              "type": "MemoryPressure"
            },
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "kubelet has no disk pressure",
              "reason": "KubeletHasNoDiskPressure",
              "status": "False",
              "type": "DiskPressure"
            },
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "kubelet has sufficient PID available",
              "reason": "KubeletHasSufficientPID",
              "status": "False",
              "type": "PIDPressure"
            },
            {
              "lastHeartbeatTime": "2021-09-07T20:37:28Z",
              "lastTransitionTime": "2021-09-07T20:37:28Z",
              "message": "[container runtime status check may not have completed yet, container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized, CSINode is not yet initialized, missing node capacity for resources: ephemeral-storage]",
              "reason": "KubeletNotReady",
              "status": "False",
              "type": "Ready"
            }
          ],
          "daemonEndpoints": {
            "kubeletEndpoint": {
              "Port": 10250
            }
          },
          "nodeInfo": {
            "architecture": "amd64",
            "bootID": "0d0dd4f2-8829-4b03-9f29-794f4908281b",
            "containerRuntimeVersion": "docker://19.3.13",
            "kernelVersion": "5.4.141-67.229.amzn2.x86_64",
            "kubeProxyVersion": "v1.21.2-eks-55daa9d",
            "kubeletVersion": "v1.21.2-eks-55daa9d",
            "machineID": "ec2483c633b0e271f36ce14e45a361b8",
            "operatingSystem": "linux",
            "osImage": "Amazon Linux 2",
            "systemUUID": "ec2483c6-33b0-e271-f36c-e14e45a361b8"
          }
        }
      },
      "responseStatus": {
        "metadata": {}
      },
      "user": {
        "extra": {}
      }
    }
  }
```

ILF Translation:

```
OCSF_600301[*,*,2024-11-20T16:45:21.994493-05:00,(actor_d_user_d_groups_d_1_d_name="system:nodes";unmapped_d_requestObject_d_status_d_daemonEndpoints_d_kubeletEndpoint_d_Port=10250;unmapped_d_requestObject_d_status_d_allocatable_d_hugepages_mi_1Gi="0";unmapped_d_requestObject_d_status_d_conditions_d_0_d_lastTransitionTime="2021-09-07T20:37:28Z";unmapped_d_requestObject_d_status_d_nodeInfo_d_architecture="amd64";unmapped_d_responseObject_d_status_d_capacity_d_memory="16093700Ki";actor_d_user_d_type_id=0;unmapped_d_requestObject_d_status_d_addresses_d_3_d_address="ip-192-001-02-03.ec2.internal";unmapped_d_requestObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_capacityType="ON_DEMAND";api_d_operation="create";start_time=1631047050502680;unmapped_d_responseObject_d_metadata_d_labels_d_kubernetes_d_io_fs_os="linux";unmapped_d_responseObject_d_status_d_conditions_d_0_d_reason="KubeletHasSufficientMemory";unmapped_d_requestObject_d_status_d_addresses_d_4_d_type="ExternalDNS";api_d_version="v1";unmapped_d_responseObject_d_status_d_addresses_d_3_d_address="ip-192-001-02-03.ec2.internal";unmapped_d_responseObject_d_status_d_allocatable_d_memory="15076868Ki";activity_id=1;unmapped_d_requestObject_d_status_d_capacity_d_hugepages_mi_1Gi="0";unmapped_d_responseObject_d_status_d_addresses_d_3_d_type="InternalDNS";unmapped_d_responseObject_d_status_d_conditions_d_0_d_status="False";unmapped_d_responseObject_d_status_d_addresses_d_4_d_address="ec2-12.000.22.33.compute-1.amazonaws.com";unmapped_d_requestObject_d_status_d_conditions_d_1_d_message="kubelet has no disk pressure";unmapped_d_responseObject_d_status_d_allocatable_d_hugepages_mi_1Gi="0";unmapped_d_requestObject_d_status_d_conditions_d_3_d_message="[container runtime status check may not have completed yet, container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized, CSINode is not yet initialized, missing node capacity for resources: ephemeral-storage]";unmapped_d_responseObject_d_status_d_nodeInfo_d_containerRuntimeVersion="docker://19.3.13";unmapped_d_requestObject_d_status_d_addresses_d_0_d_type="InternalIP";actor_d_session_d_credential_uid="EXAMPLEUIDTEST";actor_d_user_d_groups_d_2_d_name="system:authenticated";unmapped_d_requestObject_d_status_d_allocatable_d_cpu="3920m";unmapped_d_responseObject_d_status_d_conditions_d_3_d_lastHeartbeatTime="2021-09-07T20:37:28Z";unmapped_d_requestObject_d_status_d_addresses_d_0_d_address="192.000.22.33";metadata_d_product_d_vendor_name="AWS";unmapped_d_responseObject_d_metadata_d_managedFields_d_0_d_manager="kubelet";unmapped_d_responseObject_d_status_d_addresses_d_2_d_type="Hostname";unmapped_d_requestObject_d_metadata_d_labels_d_beta_d_kubernetes_d_io_fs_arch="amd64";category_name="Application Activity";unmapped_d_requestObject_d_status_d_capacity_d_cpu="4";unmapped_d_requestObject_d_status_d_conditions_d_2_d_reason="KubeletHasSufficientPID";unmapped_d_requestObject_d_status_d_conditions_d_0_d_type="MemoryPressure";unmapped_d_requestObject_d_metadata_d_labels_d_failure_mi_domain_d_beta_d_kubernetes_d_io_fs_zone="us-east-1f";unmapped_d_responseObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_nodegroup="ng-5fe434eb";unmapped_d_requestObject_d_status_d_conditions_d_3_d_reason="KubeletNotReady";unmapped_d_responseObject_d_status_d_addresses_d_4_d_type="ExternalDNS";unmapped_d_requestObject_d_spec_d_providerID="aws:///us-east-1f/i-12345678901";unmapped_d_responseObject_d_status_d_nodeInfo_d_bootID="0d0dd4f2-8829-4b03-9f29-794f4908281b";unmapped_d_responseObject_d_status_d_daemonEndpoints_d_kubeletEndpoint_d_Port=10250;unmapped_d_requestObject_d_status_d_nodeInfo_d_containerRuntimeVersion="docker://19.3.13";observables_d_0_d_type_id=4;unmapped_d_requestObject_d_status_d_conditions_d_2_d_lastHeartbeatTime="2021-09-07T20:37:28Z";unmapped_d_responseObject_d_metadata_d_labels_d_beta_d_kubernetes_d_io_fs_arch="amd64";unmapped_d_requestObject_d_status_d_conditions_d_1_d_reason="KubeletHasNoDiskPressure";time_dt="2021-09-07T20:37:30.642854+00:00";unmapped_d_requestObject_d_status_d_conditions_d_0_d_reason="KubeletHasSufficientMemory";unmapped_d_requestObject_d_status_d_capacity_d_pods="58";unmapped_d_annotations_d_authorization_d_k8s_d_io_fs_reason="";unmapped_d_requestObject_d_status_d_nodeInfo_d_systemUUID="ec2483c6-33b0-e271-f36c-e14e45a361b8";unmapped_d_responseObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_capacityType="ON_DEMAND";category_uid=6;unmapped_d_requestObject_d_metadata_d_name="ip-192-001-02-03.ec2.internal";unmapped_d_responseObject_d_metadata_d_labels_d_node_d_kubernetes_d_io_fs_instance_mi_type="m5.xlarge";unmapped_d_responseObject_d_status_d_capacity_d_cpu="4";unmapped_d_requestObject_d_metadata_d_labels_d_node_d_kubernetes_d_io_fs_instance_mi_type="m5.xlarge";unmapped_d_responseObject_d_status_d_conditions_d_0_d_message="kubelet has sufficient memory available";unmapped_d_requestObject_d_status_d_allocatable_d_pods="58";observables_d_0_d_name="actor.user.name";unmapped_d_responseObject_d_metadata_d_labels_d_alpha_d_eksctl_d_io_fs_cluster_mi_name="ABCD1234567890EXAMPLE";http_request_d_user_agent="kubelet/v1.21.2 (linux/amd64) kubernetes/729bdfc";observables_d_1_d_value="12.000.22.33";severity="Informational";unmapped_d_responseObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_sourceLaunchTemplateId="lt-0f20d6f901007611e";unmapped_d_responseObject_d_metadata_d_name="ip-192-001-02-03.ec2.internal";unmapped_d_responseObject_d_metadata_d_managedFields_d_0_d_operation="Update";unmapped_d_responseObject_d_status_d_conditions_d_2_d_message="kubelet has sufficient PID available";unmapped_d_responseObject_d_status_d_conditions_d_2_d_reason="KubeletHasSufficientPID";unmapped_d_responseObject_d_kind="Node";unmapped_d_annotations_d_authorization_d_k8s_d_io_fs_decision="allow";unmapped_d_responseObject_d_status_d_conditions_d_2_d_lastHeartbeatTime="2021-09-07T20:37:28Z";unmapped_d_responseObject_d_status_d_capacity_d_hugepages_mi_1Gi="0";observables_d_2_d_value="/api/v1/nodes";unmapped_d_responseObject_d_status_d_conditions_d_1_d_lastHeartbeatTime="2021-09-07T20:37:28Z";unmapped_d_requestObject_d_status_d_conditions_d_1_d_lastHeartbeatTime="2021-09-07T20:37:28Z";metadata_d_version="1.2.0";unmapped_d_responseObject_d_status_d_conditions_d_3_d_message="[container runtime status check may not have completed yet, container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized, CSINode is not yet initialized, missing node capacity for resources: ephemeral-storage]";metadata_d_profiles_d_1="datetime";unmapped_d_responseObject_d_status_d_addresses_d_0_d_type="InternalIP";unmapped_d_requestObject_d_metadata_d_labels_d_beta_d_kubernetes_d_io_fs_instance_mi_type="m5.xlarge";metadata_d_product_d_feature_d_name="Elastic Kubernetes Service";unmapped_d_responseObject_d_status_d_allocatable_d_pods="58";unmapped_d_responseObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_nodegroup_mi_image="ami-0193ebf9573ebc9f7";unmapped_d_requestObject_d_status_d_conditions_d_0_d_message="kubelet has sufficient memory available";unmapped_d_responseObject_d_status_d_conditions_d_1_d_reason="KubeletHasNoDiskPressure";unmapped_d_requestObject_d_status_d_nodeInfo_d_kubeProxyVersion="v1.21.2-eks-55daa9d";message="ResponseComplete";observables_d_1_d_type_="IP Address";unmapped_d_responseObject_d_apiVersion="v1";unmapped_d_requestObject_d_status_d_conditions_d_3_d_lastTransitionTime="2021-09-07T20:37:28Z";metadata_d_product_d_name="Amazon EKS";unmapped_d_requestObject_d_status_d_nodeInfo_d_kubeletVersion="v1.21.2-eks-55daa9d";unmapped_d_requestObject_d_status_d_nodeInfo_d_kernelVersion="5.4.141-67.229.amzn2.x86_64";unmapped_d_requestObject_d_status_d_addresses_d_2_d_address="ip-192-001-02-03.ec2.internal";unmapped_d_responseObject_d_status_d_nodeInfo_d_machineID="ec2483c633b0e271f36ce14e45a361b8";unmapped_d_requestObject_d_kind="Node";unmapped_d_requestObject_d_status_d_capacity_d_hugepages_mi_2Mi="0";unmapped_d_requestObject_d_status_d_allocatable_d_hugepages_mi_2Mi="0";unmapped_d_requestObject_d_apiVersion="v1";api_d_request_d_uid="f47c68f2-d3ac-4f96-b2f4-5d497bf79b64";unmapped_d_requestObject_d_metadata_d_labels_d_topology_d_kubernetes_d_io_fs_region="us-east-1";unmapped_d_requestObject_d_status_d_nodeInfo_d_bootID="0d0dd4f2-8829-4b03-9f29-794f4908281b";unmapped_d_requestObject_d_status_d_conditions_d_2_d_lastTransitionTime="2021-09-07T20:37:28Z";unmapped_d_responseObject_d_status_d_nodeInfo_d_architecture="amd64";unmapped_d_requestObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_nodegroup="ng-5fe434eb";unmapped_d_requestObject_d_status_d_conditions_d_2_d_message="kubelet has sufficient PID available";unmapped_d_responseObject_d_status_d_conditions_d_3_d_reason="KubeletNotReady";unmapped_d_responseObject_d_status_d_nodeInfo_d_kernelVersion="5.4.141-67.229.amzn2.x86_64";actor_d_user_d_groups_d_0_d_name="system:bootstrappers";severity_id=1;unmapped_d_responseObject_d_status_d_conditions_d_3_d_status="False";unmapped_d_responseObject_d_metadata_d_uid="4ecf628a-1b50-47ed-932c-bb1df89dad10";unmapped_d_requestObject_d_status_d_capacity_d_memory="16093700Ki";observables_d_2_d_type_id=6;unmapped_d_requestObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_sourceLaunchTemplateVersion="1";unmapped_d_responseObject_d_status_d_conditions_d_2_d_type="PIDPressure";unmapped_d_responseObject_d_status_d_nodeInfo_d_osImage="Amazon Linux 2";unmapped_d_requestObject_d_status_d_addresses_d_1_d_address="12.000.22.33";actor_d_user_d_name="system:node:ip-192-001-02-03.ec2.internal";unmapped_d_responseObject_d_metadata_d_annotations_d_volumes_d_kubernetes_d_io_fs_controller_mi_managed_mi_attach_mi_detach="true";unmapped_d_kind="Event";unmapped_d_responseObject_d_metadata_d_labels_d_alpha_d_eksctl_d_io_fs_nodegroup_mi_name="ng-5fe434eb";unmapped_d_responseObject_d_metadata_d_managedFields_d_0_d_fieldsType="FieldsV1";observables_d_0_d_type_="User Name";unmapped_d_requestObject_d_status_d_conditions_d_1_d_status="False";unmapped_d_requestObject_d_status_d_conditions_d_3_d_type="Ready";unmapped_d_requestObject_d_status_d_conditions_d_0_d_status="False";unmapped_d_requestObject_d_status_d_nodeInfo_d_osImage="Amazon Linux 2";unmapped_d_responseObject_d_metadata_d_managedFields_d_0_d_apiVersion="v1";resources_d_0_d_name="ip-192-001-02-03.ec2.internal";unmapped_d_requestObject_d_status_d_nodeInfo_d_operatingSystem="linux";unmapped_d_responseObject_d_status_d_conditions_d_1_d_lastTransitionTime="2021-09-07T20:37:28Z";actor_d_user_d_uid="heptio-authenticator-aws:123456789012:ABCD1234567890EXAMPLE";unmapped_d_responseObject_d_status_d_addresses_d_2_d_address="ip-192-001-02-03.ec2.internal";unmapped_d_requestObject_d_metadata_d_labels_d_failure_mi_domain_d_beta_d_kubernetes_d_io_fs_region="us-east-1";unmapped_d_requestObject_d_metadata_d_labels_d_beta_d_kubernetes_d_io_fs_os="linux";time=1631047050642854;type_uid=600301;observables_d_1_d_type_id=2;unmapped_d_responseObject_d_status_d_conditions_d_1_d_message="kubelet has no disk pressure";unmapped_d_responseObject_d_metadata_d_labels_d_failure_mi_domain_d_beta_d_kubernetes_d_io_fs_zone="us-east-1f";unmapped_d_responseObject_d_metadata_d_labels_d_kubernetes_d_io_fs_arch="amd64";unmapped_d_responseObject_d_status_d_allocatable_d_attachable_mi_volumes_mi_aws_mi_ebs="25";actor_d_session_d_issuer="arn:aws:iam::123456789012:role/example-test-161366663-NodeInstanceRole-abc12345678912";observables_d_1_d_name="src_endpoint.ip";api_d_response_d_code=201;start_time_dt="2021-09-07T20:37:30.502680+00:00";unmapped_d_responseObject_d_spec_d_taints_d_0_d_effect="NoSchedule";unmapped_d_responseObject_d_status_d_nodeInfo_d_systemUUID="ec2483c6-33b0-e271-f36c-e14e45a361b8";unmapped_d_responseObject_d_status_d_allocatable_d_hugepages_mi_2Mi="0";unmapped_d_responseObject_d_metadata_d_creationTimestamp="2021-09-07T20:37:30Z";unmapped_d_requestObject_d_metadata_d_annotations_d_volumes_d_kubernetes_d_io_fs_controller_mi_managed_mi_attach_mi_detach="true";unmapped_d_requestObject_d_status_d_addresses_d_4_d_address="ec2-12.000.22.33.compute-1.amazonaws.com";unmapped_d_responseObject_d_status_d_conditions_d_0_d_lastHeartbeatTime="2021-09-07T20:37:28Z";unmapped_d_requestObject_d_status_d_addresses_d_1_d_type="ExternalIP";unmapped_d_responseObject_d_status_d_capacity_d_pods="58";unmapped_d_requestObject_d_status_d_allocatable_d_memory="15076868Ki";unmapped_d_requestObject_d_status_d_conditions_d_3_d_lastHeartbeatTime="2021-09-07T20:37:28Z";unmapped_d_responseObject_d_metadata_d_managedFields_d_0_d_time="2021-09-07T20:37:30Z";unmapped_d_requestObject_d_metadata_d_labels_d_topology_d_kubernetes_d_io_fs_zone="us-east-1f";unmapped_d_responseObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_sourceLaunchTemplateVersion="1";unmapped_d_requestObject_d_status_d_conditions_d_3_d_status="False";unmapped_d_responseObject_d_status_d_conditions_d_1_d_type="DiskPressure";unmapped_d_requestObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_nodegroup_mi_image="ami-0193ebf9573ebc9f7";unmapped_d_responseObject_d_status_d_capacity_d_attachable_mi_volumes_mi_aws_mi_ebs="25";unmapped_d_responseObject_d_metadata_d_labels_d_kubernetes_d_io_fs_hostname="ip-192-001-02-03.ec2.internal";unmapped_d_responseObject_d_status_d_nodeInfo_d_kubeletVersion="v1.21.2-eks-55daa9d";unmapped_d_responseObject_d_status_d_capacity_d_hugepages_mi_2Mi="0";unmapped_d_responseObject_d_status_d_addresses_d_0_d_address="192.000.22.33";unmapped_d_responseObject_d_status_d_conditions_d_0_d_type="MemoryPressure";unmapped_d_requestObject_d_status_d_allocatable_d_attachable_mi_volumes_mi_aws_mi_ebs="25";http_request_d_url_d_path="/api/v1/nodes";unmapped_d_requestObject_d_status_d_capacity_d_attachable_mi_volumes_mi_aws_mi_ebs="25";unmapped_d_responseObject_d_status_d_allocatable_d_cpu="3920m";class_uid=6003;type_name="API Activity: Create";metadata_d_log_level="RequestResponse";unmapped_d_responseObject_d_status_d_conditions_d_3_d_lastTransitionTime="2021-09-07T20:37:28Z";unmapped_d_requestObject_d_metadata_d_labels_d_kubernetes_d_io_fs_hostname="ip-192-001-02-03.ec2.internal";unmapped_d_requestObject_d_metadata_d_labels_d_alpha_d_eksctl_d_io_fs_cluster_mi_name="ABCD1234567890EXAMPLE";cloud_d_provider="AWS";class_name="API Activity";unmapped_d_requestObject_d_status_d_conditions_d_0_d_lastHeartbeatTime="2021-09-07T20:37:28Z";unmapped_d_responseObject_d_status_d_conditions_d_3_d_type="Ready";metadata_d_product_d_version="audit.k8s.io/v1";unmapped_d_responseObject_d_status_d_addresses_d_1_d_type="ExternalIP";unmapped_d_responseObject_d_metadata_d_labels_d_failure_mi_domain_d_beta_d_kubernetes_d_io_fs_region="us-east-1";observables_d_2_d_name="http_request.url.path";unmapped_d_responseObject_d_status_d_conditions_d_1_d_status="False";activity_name="Create";unmapped_d_responseObject_d_status_d_conditions_d_0_d_lastTransitionTime="2021-09-07T20:37:28Z";unmapped_d_requestObject_d_status_d_addresses_d_3_d_type="InternalDNS";unmapped_d_responseObject_d_status_d_nodeInfo_d_operatingSystem="linux";unmapped_d_requestObject_d_status_d_nodeInfo_d_machineID="ec2483c633b0e271f36ce14e45a361b8";unmapped_d_responseObject_d_status_d_conditions_d_2_d_status="False";unmapped_d_requestObject_d_metadata_d_labels_d_kubernetes_d_io_fs_os="linux";cloud_d_account_d_uid="arn:aws:sts::123456789012:assumed-role/example-test-161366663-NodeInstanceRole-abc12345678912/i-12345678901";observables_d_2_d_type_="URL String";unmapped_d_responseObject_d_spec_d_providerID="aws:///us-east-1f/i-12345678901";unmapped_d_requestObject_d_status_d_conditions_d_1_d_lastTransitionTime="2021-09-07T20:37:28Z";unmapped_d_responseObject_d_status_d_nodeInfo_d_kubeProxyVersion="v1.21.2-eks-55daa9d";actor_d_session_d_uid="i-12345678901";metadata_d_profiles_d_0="cloud";unmapped_d_requestObject_d_status_d_addresses_d_2_d_type="Hostname";unmapped_d_responseObject_d_spec_d_taints_d_0_d_key="node.kubernetes.io/not-ready";unmapped_d_requestObject_d_metadata_d_labels_d_eks_d_amazonaws_d_com_fs_sourceLaunchTemplateId="lt-0f20d6f901007611e";unmapped_d_responseObject_d_metadata_d_labels_d_topology_d_kubernetes_d_io_fs_zone="us-east-1f";unmapped_d_responseObject_d_metadata_d_resourceVersion="67933403";unmapped_d_requestObject_d_metadata_d_labels_d_kubernetes_d_io_fs_arch="amd64";unmapped_d_requestObject_d_metadata_d_labels_d_alpha_d_eksctl_d_io_fs_nodegroup_mi_name="ng-5fe434eb";resources_d_0_d_type_="nodes";src_endpoint_d_ip="12.000.22.33";unmapped_d_responseObject_d_metadata_d_labels_d_beta_d_kubernetes_d_io_fs_os="linux";unmapped_d_responseObject_d_metadata_d_labels_d_beta_d_kubernetes_d_io_fs_instance_mi_type="m5.xlarge";unmapped_d_responseObject_d_status_d_addresses_d_1_d_address="12.000.22.33";unmapped_d_responseObject_d_status_d_conditions_d_2_d_lastTransitionTime="2021-09-07T20:37:28Z";unmapped_d_requestObject_d_status_d_conditions_d_1_d_type="DiskPressure";observables_d_0_d_value="system:node:ip-192-001-02-03.ec2.internal";unmapped_d_responseObject_d_metadata_d_labels_d_topology_d_kubernetes_d_io_fs_region="us-east-1";unmapped_d_requestObject_d_status_d_conditions_d_2_d_type="PIDPressure";unmapped_d_requestObject_d_status_d_conditions_d_2_d_status="False";)] 
```
