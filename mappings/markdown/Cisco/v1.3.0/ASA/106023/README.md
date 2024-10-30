# Event Dossier: Cisco ASA 106023

### A 106023 event

- **Description**: Translates a Cisco ASA 106023 Event to OCSF.
- **Event References**:
    - https://www.cisco.com/c/en/us/td/docs/security/asa/syslog/b_syslog/syslog-messages-101001-to-199021.html#con_6482625

### OCSF Version: 1.3.0

- `activity_id`: 5,
- `activity_name`: `Refuse`,
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
- `severity`: `Critical`
- `severity_id`: `5`
- `status`: `Failure`
- `status_id`: `2`
- `type_name`: `Network Activity: Refuse`
- `type_uid`: `400105`

### Parsing:

- Parsing the Syslog and ASA header using `grok`:

```
%{GREEDYDATA:timestamp} %{HOSTNAME:hostname} %{WORD:program}\[%{POSINT:pid}\]: %ASA-%{INT:level}-%{INT:message_number}: %{GREEDYDATA:message_text}
```

This produces:

```json
  {
  "hostname": "localhost",
  "message_text": "Deny tcp src outside:100.66.19.254/80 dst inside:172.31.98.44/8277 by access-group \"inbound\" [0x0, 0x0]",
  "level": "4",
  "message_number": "106023",
  "__raw__": "Oct 10 2018 12:34:56 localhost CiscoASA[999]: %ASA-4-106023: Deny tcp src outside:100.66.19.254/80 dst inside:172.31.98.44/8277 by access-group \"inbound\" [0x0, 0x0]",
  "pid": "999",
  "program": "CiscoASA",
  "timestamp": "Oct 10 2018 12:34:56"
}
```

- Parsing the 106023 message text using `gork`

```
Deny %{WORD:protocol} src %{WORD:source_interface}:%{IP:source_ip}/%{NUMBER:source_port} dst %{WORD:dest_interface}:%{IP:dest_ip}/%{NUMBER:dest_port} by access-group %{DATA:access_group} \[%{DATA:rule_ids}\]
```

This produces:

```json
{
  "level": "4",
  "dest_interface": "inside",
  "message_number": "106023",
  "__raw__": "Oct 10 2018 12:34:56 localhost CiscoASA[999]: %ASA-4-106023: Deny tcp src outside:100.66.19.254/80 dst inside:172.31.98.44/8277 by access-group \"inbound\" [0x0, 0x0]",
  "pid": "999",
  "program": "CiscoASA",
  "source_ip": "100.66.19.254",
  "hostname": "localhost",
  "protocol": "tcp",
  "rule_ids": "0x0, 0x0",
  "source_interface": "outside",
  "source_port": "80",
  "dest_ip": "172.31.98.44",
  "access_group": "\"inbound\"",
  "dest_port": "8277",
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
| `src_endpoint.interface`        | `source_interface`                                     |
| `dst_endpoint.ip`               | `dest_ip`                                              |
| `dst_endpoint.port`             | `dest_port`                                            |
| `dst_endpoint.interface`        | `dest_interface`                                       |
| `connection_info.protocol_name` | `protocol`                                             |
| `metadata.event_code`           | `message_number`                                       |
| `metadata.original_time`        | `timestamp`                                            |
| `unmapped.rule_ids`             | `rule_ids`                                             |
| `unmapped.program`              | `program`                                              |
| `unmapped.pid`                  | `pid`                                                  |

> **_NOTE:_**\
> `ts_str_to_epoch` parses given timestamp string into echo milliseconds