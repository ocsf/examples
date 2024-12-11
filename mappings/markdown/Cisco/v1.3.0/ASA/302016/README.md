# Event Dossier: Cisco ASA 302016

### A 302016 event

- **Description**: Translates a Cisco ASA 302016 Event to OCSF.
- **Event References**:
    - https://www.cisco.com/c/en/us/td/docs/security/asa/syslog/b_syslog/syslog-messages-302003-to-342008.html#con_4770749

### OCSF Version: 1.3.0

- `activity_id`: 2,
- `activity_name`: `Close`,
- `category_name`: `Network Activity`
- `category_uid`: `4`
- `class_name`: `Network Activity`
- `class_uid`: `4001`
- `connection_info.boundary`: `External`
- `connection_info.boundary_id`: `3`
- `connection_info.direction`: `Inbound`
- `connection_info.direction_id`: `1`
- `metadata.product.name`: `Cisco ASA`
- `metadata.product.vendor_name`: `Cisco`
- `metadata.product.version`: `Unknown`
- `metadata.version`: `1.3.0`
- `severity`: `Informational`
- `severity_id`: `1`
- `status`: `Success`
- `status_id`: `1`
- `type_name`: `Network Activity: Close`
- `type_uid`: `400102`

### Parsing:

- Parsing the Syslog and ASA header using `grok`:

```
%{GREEDYDATA:timestamp} %{HOSTNAME:hostname} %{WORD:program}\[%{POSINT:pid}\]: %ASA-%{INT:level}-%{INT:message_number}: %{GREEDYDATA:message_text}
```

This produces:

```json
{
  "hostname": "localhost",
  "message_text": "Teardown UDP connection 11758 for outside:100.66.80.32/53 to inside:172.31.98.44/56132 duration 0:00:00 bytes 148",
  "level": "6",
  "message_number": "302016",
  "__raw__": "Oct 10 2018 12:34:56 localhost CiscoASA[999]: %ASA-6-302016: Teardown UDP connection 11758 for outside:100.66.80.32/53 to inside:172.31.98.44/56132 duration 0:00:00 bytes 148",
  "pid": "999",
  "program": "CiscoASA",
  "timestamp": "Oct 10 2018 12:34:56"
}
```

- Parsing the 302016 message text using `grok`

```
Teardown %{WORD:protocol} connection %{NUMBER:connection_id} for %{DATA:source_interface}:%{IP:source_ip}/%{NUMBER:source_port} to %{DATA:dest_interface}:%{IPORHOST:dest_ip}/%{NUMBER:dest_port} duration %{TIME:duration} bytes %{NUMBER:bytes}
```

This produces:

```json
{
  "level": "6",
  "dest_interface": "inside",
  "message_number": "302016",
  "__raw__": "Oct 10 2018 12:34:56 localhost CiscoASA[999]: %ASA-6-302016: Teardown UDP connection 11758 for outside:100.66.80.32/53 to inside:172.31.98.44/56132 duration 0:00:00 bytes 148",
  "pid": "999",
  "program": "CiscoASA",
  "source_ip": "100.66.80.32",
  "duration": "0:00:00",
  "hostname": "localhost",
  "protocol": "UDP",
  "connection_id": "11758",
  "source_interface": "outside",
  "bytes": "148",
  "source_port": "53",
  "dest_ip": "172.31.98.44",
  "dest_port": "56132",
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
| `connection_info.uid`           | `connection_id`                                        |
| `duration`                      | `duration_str_to_mills($.duration)`                    |
| `metadata.event_code`           | `message_number`                                       |
| `metadata.original_time`        | `timestamp`                                            |
| `traffic.bytes`                 | `bytes`                                                |
| `unmapped.program`              | `program`                                              |
| `unmapped.pid`                  | `pid`                                                  |

> **_NOTE:_**\
> `ts_str_to_epoch` parses given timestamp string into echo milliseconds\
> `duration_str_to_mills($.duration)` parses given duration string (must match the pattern of `HH:mm:ss`) into
> milliseconds