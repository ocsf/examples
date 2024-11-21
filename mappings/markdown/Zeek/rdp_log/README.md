# Event Dossier: Zeek rdp.log
### Summary:
- **Description**: Translates a Zeek rdp.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/rdp_activity
  - https://docs.zeek.org/en/master/logs/rdp.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/rdp/main.zeek.html#type-RDP::Info
    
 ### Static mapping: OCSF Version: 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `RDP Activity`
 - `class_uid`: `4007`
 - `metadata.log_name`: `rdp.log`
 - `metadata.loggers[].log_provider`: `Zeek`
 - `metadata.loggers[].product.name`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `rdp.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/rdp.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`
 - `dst_endpoint.agent_list.type`: `Remote Access`
 - `dst_endpoint.agent_list.type_id`: `9`
 - `src_endpoint.agent_list.type`: `Remote Access`
 - `src_endpoint.agent_list.type_id`: `9`

 ### Mapping:

| OCSF                           | Raw                    | Zeek Field Description                                                                  |
| ------------------------------ | ---------------------- | --------------------------------------------------------------------------------------- |
| `time`                         | `ts`                   | Timestamp indicating when the event occurred.                                           |
| `start_time`                   | `ts`                   | Timestamp indicating when the event occurred.                                           |
| `metadata.logged_time`         | `_write_ts`            | Timestamp indicating when the log entry was written to disk.                            |
| `metadata.loggers[].name`      | `_system_name`         | Name of the system or logging subsystem generating the log entry.                       |
| `metadata.uid`                 | `uid`                  | Unique ID for the connection.                                                           |
| `src_endpoint.ip`              | `id.orig_h`            | The originator’s IP address.                                                            |
| `src_endpoint.port`            | `id.orig_p`            | The originator’s port number.                                                           |
| `src_endpoint.hostname`        | `client_name`          | Name of the client machine.                                                             |
| `src_endpoint.agent_list.name` | `client_build`         | RDP client version used by the client machine.                                          |
| `src_endpoint.agent_list.version` | `client_dig_product_id` | Product ID of the client machine.                                                   |
| `dst_endpoint.ip`              | `id.resp_h`            | The responder’s IP address.                                                             |
| `dst_endpoint.port`            | `id.resp_p`            | The responder’s port number.                                                            |
| `identifier_cookie`            | `cookie`               | Cookie value used by the client machine.                                                |
| `protocol_ver`                 | `security_protocol`    | Security protocol chosen by the server.                                                 |
| `status_detail`                | `result`               | Status result for the connection.                                                       |
| `tls.key_length`               | `encryption_method`    | Encryption method of the connection.                                                    |
| `remote_display.color_depth`   | `requested_color_depth`| The color depth requested by the client in the high_color_depth field.                  |
| `remote_display.physical_height` | `desktop_height`     | Desktop height of the client machine.                                                   |
| `remote_display.physical_width`| `desktop_width`        | Desktop width of the client machine.                                                    |

 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Evaluation Conditions                         | Zeek Field Description                                                                  |
| ------------------------------ | ----------------- | --------------------------------------------- | --------------------------------------------------------------------------------------- |
| `observables[].value`          | `rdfp_hash`       | Where `observables[].type_id` = "30"          | The rdfp_hash information.                                                              |
| `observables[].value`          | `rdfp_string`     | Where `observables[].type_id` = "99"          | A fingerprint which represents an RDP client.                                           |
| `observables[].value`          | `keyboard_layout` | Where `observables[].type_id` = "99"          | Keyboard layout (language) of the client machine.                                       |

 ### Unmapped:
| OCSF                     | Raw                | Zeek Field Description                                                                  |
| -------------------------| -------------------| --------------------------------------------------------------------------------------- |
| `unmapped`               | `cert_count`       | The number of certs seen.                                                               |
| `unmapped`               | `cert_permanent`   | Indicates if the provided certificate or certificate chain is permanent or temporary.   |
| `unmapped`               | `cert_type`        | If the connection is being encrypted with native RDP encryption, this is the type of cert being used. |
| `unmapped`               | `channels_joined`  | The number of channels a client joined during the connection sequence.                  |
| `unmapped`               | `client_channels`  | The channels requested by the client.                                                   |
| `unmapped`               | `encryption_level` | Encryption level of the connection.                                                     |
