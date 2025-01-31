# Event Dossier: Cisco ASA 305011

### A 305011 event

- **Description**: Translates a Cisco ASA 305011 Event to OCSF.
- **Event References**:
    - https://www.cisco.com/c/en/us/td/docs/security/asa/syslog/b_syslog/syslog-messages-302003-to-342008.html#con_4771036

### OCSF Version: 1.3.0

- `activity_id`: 1,
- `activity_name`: `Open`,
- `category_name`: `Network Activity`
- `category_uid`: `4`
- `class_name`: `Network Activity`
- `class_uid`: `4001`
- `connection_info.boundary`: `External`
- `connection_info.boundary_id`: `3`
- `connection_info.direction`: `Outbound`
- `connection_info.direction_id`: `2`
- `metadata.product.name`: `Cisco ASA`
- `metadata.product.vendor_name`: `Cisco`
- `metadata.product.version`: `Unknown`
- `metadata.version`: `1.3.0`
- `severity`: `Informational`
- `severity_id`: `1`
- `status`: `Success`
- `status_id`: `1`
- `type_name`: `Network Activity: Open`
- `type_uid`: `400101`

### Parsing:

- Parsing the Syslog and ASA header using `grok`:

```
%{GREEDYDATA:timestamp} %{HOSTNAME:hostname} %{WORD:program}\[%{POSINT:pid}\]: %ASA-%{INT:level}-%{INT:message_number}: %{GREEDYDATA:message_text}
```

This produces:

```json
{
  "hostname": "localhost",
  "message_text": "Built dynamic TCP translation from inside:172.31.98.44/1772 to outside:100.66.98.44/8256",
  "level": "6",
  "message_number": "305011",
  "__raw__": "Oct 10 2018 12:34:56 localhost CiscoASA[999]: %ASA-6-305011: Built dynamic TCP translation from inside:172.31.98.44/1772 to outside:100.66.98.44/8256",
  "pid": "999",
  "program": "CiscoASA",
  "timestamp": "Oct 10 2018 12:34:56"
}
```

- Parsing the 305011 message text using `grok`

```
%{WORD:action} %{WORD:translation_type} %{WORD:protocol} translation from %{WORD:source_interface}:%{IP:source_ip}/%{INT:source_port} to %{WORD:dest_interface}:%{IP:dest_ip}/%{INT:dest_port}
```

This produces:

```json
{
  "level": "6",
  "message_number": "305011",
  "source_interface": "inside",
  "__raw__": "Oct 10 2018 12:34:56 localhost CiscoASA[999]: %ASA-6-305011: Built dynamic TCP translation from inside:172.31.98.44/1772 to outside:100.66.98.44/8256",
  "pid": "999",
  "program": "CiscoASA",
  "dest_interface": "outside",
  "source_ip": "172.31.98.44",
  "translation_type": "dynamic",
  "hostname": "localhost",
  "protocol": "TCP",
  "source_port": "1772",
  "dest_ip": "100.66.98.44",
  "action": "Built",
  "dest_port": "8256",
  "timestamp": "Oct 10 2018 12:34:56"
}
```

### Mapping:

- This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be
  necessary for a correct representation in OCSF that matches all requirements.

- Any fields not present in an explicit mapping will be mapped to the unmapped object.

| OCSF                            | Raw                                                    |
|---------------------------------|--------------------------------------------------------|
| `time`                          | `ts_str_to_epoch($.timestamp, "MMM dd yyyy HH:mm:ss")` |
| `raw_data`                      | `__raw__`                                              |
| `src_endpoint.ip`               | `source_ip`                                            |
| `src_endpoint.port`             | `source_port`                                          |
| `src_endpoint.interface_name`   | `source_interface`                                     |
| `dst_endpoint.ip`               | `dest_ip`                                              |
| `dst_endpoint.port`             | `dest_port`                                            |
| `dst_endpoint.interface_name`   | `dest_interface`                                       |
| `connection_info.protocol_name` | `protocol`                                             |
| `metadata.event_code`           | `message_number`                                       |
| `metadata.original_time`        | `timestamp`                                            |
| `unmapped.program`              | `program`                                              |
| `unmapped.pid`                  | `pid`                                                  |

> **_NOTE:_**\
> `ts_str_to_epoch` parses given timestamp string into echo milliseconds\