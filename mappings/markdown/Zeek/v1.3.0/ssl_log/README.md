# Event Dossier: Zeek ssl.log
### Summary:
- **Description**: Translates a Zeek ssl.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/ssl.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssl/main.zeek.html#type-SSL::Info

 ### OCSF Version: v1.3.0
 

  ### Static value mapping:
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.3.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4001         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |


 ### Direct field mapping:
| OCSF                           | Raw                         | Zeek Field Description                                                                  | Notes                   |
| ------------------------------ | --------------------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                         | `ts`                        | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is timestamp_t (Long). |
| `start_time`                   | `ts`                        | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is timestamp_t (Long). |
| `metadata.logged_time`         | `_write_ts`                 | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is timestamp_t (Long). |
| `metadata.loggers[].name`      | `_system_name`              | Name of the system or logging subsystem generating the log entry.                       |                         |
| `metadata.log_name`            | `_path`                     | Log name.                                                                               |                         |
| `metadata.uid`                 | `uid`                       | Unique ID for the connection.                                                           |                         |
| `src_endpoint.ip`              | `id.orig_h`                 | The originator’s IP address.                                                            | Type is ip_t.           |
| `src_endpoint.port`            | `id.orig_p`                 | The originator’s port number.                                                           | Type is port_t (Integer). |
| `dst_endpoint.ip`              | `id.resp_h`                 | The responder’s IP address.                                                             | Type is ip_t.           |
| `dst_endpoint.port`            | `id.resp_p`                 | The responder’s port number.                                                            | Type is port_t (Integer). |
| `status_detail`                | `validation_status`         | Result of certificate validation for this connection.                                   |                         |
| `tls.cipher`                   | `cipher`                    | SSL/TLS cipher suite that the server chose.                                             |                         |
| `tls.certificate.subject`      | `subject`                   | SSL subject string.                                                                     |                         |
| `tls.certificate.issuer`       | `issuer`                    | SSL issuer string.                                                                      |                         |
| `tls.ja3_hash.value`           | `ja3`                       | The ja3 information.                                                                    |                         |
| `tls.ja3s_hash.value`          | `ja3s`                      | The ja3s information.                                                                   |                         |
| `tls.sni`                      | `server_name`               | Value of the Server Name Indicator SSL/TLS extension.                                   |                         |
| `tls.version`                  | `version`                   | SSL/TLS version that the server chose.                                                  | Type is String.         |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Evaluation Conditions | Zeek Field Description                                                                 |
| ------------------------------ | ----------------- | ----------------------| -------------------------------------------------------------------------------------- |
| `activity_id`                  | `established`     | Dynamically map to activity_id based on value of `established` field. | Flag to indicate if this SSL session has been established successfully, or if it was aborted during the handshake. |
| `tls.certificate.fingerprints[].algorithm_id` | 0  | If `tls.certificate.issuer` exists, `tls.certificate.fingerprints[].algorithm_id` = 0, <br>else do not create `tls.certificate.fingerprints[].value`. <br>Type is Integer. | Zeek SSL logs do not contain the certificate fingerprint. Certificate details are sent via the X509 log. |
| `tls.certificate.fingerprints[].value` | "NULL"    | If `tls.certificate.issuer` exists, `tls.certificate.fingerprints[].value` = "NULL", <br>else do not create `tls.certificate.fingerprints[].value`. | Zeek SSL logs do not contain the certificate fingerprint. Certificate details are sent via the X509 log. |
| `tls.certificate.serial_number` | "NULL"           | If `tls.certificate.issuer` exists, `tls.certificate.serial_number` = "NULL", <br>else do not create `tls.certificate.serial_number`. | Zeek SSL logs do not contain the certificate serial number. Certificate details are sent via the X509 log. |
| `tls.ja3_hash.algorithm_id`    | 1                 | If `ja3` exists, `tls.ja3_hash.algorithm_id` = 1, <br>else do not create `tls.ja3_hash.algorithm_id`. <br>Type is Integer. | The ja3 algorithm information (MD5). |
| `tls.ja3s_hash.algorithm_id`   | 1                 | If `ja3s` exists, `tls.ja3s_hash.algorithm_id` = 1, <br>else do not create `tls.ja3s_hash.algorithm_id`. <br>Type is Integer. | The ja3s algorithm information (MD5). |
| `type_uid`                     | `class_uid` + `activity_id` | N/A         | Calculate with: (`class_uid` * 100) + `activity_id`. <br>Type is long_t.               |


 ### Unmapped (proposed):
| OCSF                     | Raw                                      | Zeek Field Description                                                                 |
| -------------------------| -----------------------------------------| -------------------------------------------------------------------------------------- |
| `connection_info.session.(history)` | `ssl_history` && `established` && `resumed` | SSL history showing which types of packets we received in which order.   |
| `tls.certificate(s[]).fingerprints[].value (client)` | `client_cert_chain_fps` | An ordered vector of all certificate fingerprints for the certificates offered by the client. |
| `tls.certificate(s[]).fingerprints[].value (server)` | `cert_chain_fps`        | An ordered vector of all certificate fingerprints for the certificates offered by the server. |
| `unmapped`               | `last_alert`                             | Last alert that was seen during the connection.                                        |
| `unmapped`               | `curve`                                  | Elliptic curve the server chose when using ECDH/ECDHE.                                 |
| `unmapped`               | `next_protocol`                          | Next protocol the server chose using the application layer next protocol extension, if present. |
| `unmapped`               | `sni_matches_cert`                       | Set to true if the hostname sent in the SNI matches the certificate.                   |
