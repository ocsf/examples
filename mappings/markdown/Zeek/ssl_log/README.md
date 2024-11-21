# Event Dossier: Zeek ssl.log
### Summary:
- **Description**: Translates a Zeek ssl.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/ssl.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssl/main.zeek.html#type-SSL::Info


 ### Static mapping: OCSF Version 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `Network Activity`
 - `class_uid`: `4001`
 - `metadata.log_name`: `ssl.log`
 - `metadata.loggers[].log_provider`: `Zeek`
 - `metadata.loggers[].product.name`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `ssl.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/ssl.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`


 ### Mapping:
| OCSF                           | Raw                         | Zeek Field Description                                                                  |
| ------------------------------ | --------------------------- | --------------------------------------------------------------------------------------- |
| `time`                         | `ts`                        | Timestamp indicating when the event occurred.                                           |
| `start_time`                   | `ts`                        | Timestamp indicating when the event occurred.                                           |
| `metadata.logged_time`         | `_write_ts`                 | Timestamp indicating when the log entry was written to disk.                            |
| `metadata.loggers[].name`      | `_system_name`              | Name of the system or logging subsystem generating the log entry.                       |
| `metadata.uid`                 | `uid`                       | Unique ID for the connection.                                                           |
| `src_endpoint.ip`              | `id.orig_h`                 | The originator’s IP address.                                                            |
| `src_endpoint.port`            | `id.orig_p`                 | The originator’s port number.                                                           |
| `dst_endpoint.ip`              | `id.resp_h`                 | The responder’s IP address.                                                             |
| `dst_endpoint.port`            | `id.resp_p`                 | The responder’s port number.                                                            |
| `tls.alert`                    | `last_alert`                | Last alert that was seen during the connection.                                         |
| `tls.cipher`                   | `cipher`                    | SSL/TLS cipher suite that the server chose.                                             |
| `tls.certificate.is_self_signed` | `validation_status`       | Result of certificate validation for this connection.                                   |
| `tls.certificate.subject`      | `subject`                   | SSL subject string.                                                                     |
| `tls.certificate.issuer`       | `issuer`                    | SSL issuer string.                                                                      |
| `tls.ja3_hash`                 | `ja3`                       | The ja3 information.                                                                    |
| `tls.ja3s_hash`                | `ja3s`                      | The ja3s information.                                                                   |
| `tls.sni`                      | `server_name`               | Value of the Server Name Indicator SSL/TLS extension.                                   |
| `tls.version`                  | `version`                   | SSL/TLS version that the server chose.                                                  |

 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Evaluation Conditions | Zeek Field Description                                                                 |
| ------------------------------ | ----------------- | ----------------------| -------------------------------------------------------------------------------------- |
| `activity_id`                  | `established`     | Dynamically map to activity_id based on value of `established` field. | Flag to indicate if this SSL session has been established successfully, or if it was aborted during the handshake. |

 ### Unmapped (proposed):
| OCSF                     | Raw                                      | Zeek Field Description                                                                 |
| -------------------------| -----------------------------------------| --------------------------------------------------------------------------------------- |
| `connection_info.session.(history)` | `ssl_history` && `established` && `resumed` | SSL history showing which types of packets we received in which order.                 |
| `tls.certificate.fingerprints.value (client)` | `client_cert_chain_fps` | An ordered vector of all certificate fingerprints for the certificates offered by the client. |
| `tls.certificate.fingerprints.value (server)` | `cert_chain_fps`        | An ordered vector of all certificate fingerprints for the certificates offered by the server. |
| `unmapped`               | `curve`                                  | Elliptic curve the server chose when using ECDH/ECDHE.                                 |
| `unmapped`               | `next_protocol`                          | Next protocol the server chose using the application layer next protocol extension, if present. |
| `unmapped`               | `sni_matches_cert`                       | Set to true if the hostname sent in the SNI matches the certificate.                   |
