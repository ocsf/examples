# Event Dossier: Zeek ssh.log
### Summary:
- **Description**: Translates a Zeek ssh.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/ssh_activity
  - https://docs.zeek.org/en/master/logs/ssh.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssh/main.zeek.html#type-SSH::Info
    
 ### OCSF Version: v1.3.0

 ### Static mapping:
| OCSF field                          | Value                                           |
| ----------------------------------- | ----------------------------------------------- |
| `metadata.version`                  | "1.3.0"                                         |
| `category_name`                     | "Network Activity"                              |
| `category_uid`                      | "4"                                             |
| `class_name`                        | "SSH Activity"                                  |
| `class_uid`                         | "4007"                                          |
| `metadata.log_name`                 | "ssh.log"                                       |
| `metadata.product.cpe_name`         | "cpe:2.3:a:zeek:zeek"                           |
| `metadata.product.feature.name`     | "ssh.log"                                       |
| `metadata.product.name`             | "Zeek"                                          |
| `metadata.product.url_string`       | "https://docs.zeek.org/en/current/logs/ssh.html"|
| `metadata.product.vendor_name`      | "Zeek"                                          |
| `severity`                          | "Informational"                                 |
| `severity_id`                       | "1"                                             |
| `dst_endpoint.agent_list[].type`    | "Remote Access"                                 |
| `dst_endpoint.agent_list[].type_id` | "9"                                             |
| `src_endpoint.agent_list[].type`    | "Remote Access"                                 |
| `src_endpoint.agent_list[].type_id` | "9"                                             |

 ### Mapping:
| OCSF                           | Raw                         | Zeek Field Description                                                                  |
| ------------------------------ | --------------------------- | --------------------------------------------------------------------------------------- |
| `time`                         | `ts`                        | Timestamp indicating when the event occurred. (Convert to epoch value)                  |
| `start_time`                   | `ts`                        | Timestamp indicating when the event occurred. (Convert to epoch value)                  |
| `metadata.logged_time`         | `_write_ts`                 | Timestamp indicating when the log entry was written to disk. (Convert to epoch value)   |
| `metadata.loggers[].name`      | `_system_name`              | Name of the system or logging subsystem generating the log entry.                       |
| `metadata.uid`                 | `uid`                       | Unique ID for the connection.                                                           |
| `src_endpoint.ip`              | `id.orig_h`                 | The originator’s IP address.                                                            |
| `src_endpoint.port`            | `id.orig_p`                 | The originator’s port number.                                                           |
| `src_endpoint.agent_list[].name` | `client`                  | The client’s version string.                                                            |
| `src_endpoint.location.city`   | `remote_location.city`      | The city.                                                                               |
| `src_endpoint.location.country`| `remote_location.country_code` | The country code.                                                                    |
| `src_endpoint.location.lat`    | `remote_location.latitude`  | Latitude.                                                                               |
| `src_endpoint.location.long`   | `remote_location.longitude` | Longitude.                                                                              |
| `src_endpoint.location.region` | `remote_location.region`    | The region.                                                                             |
| `dst_endpoint.ip`              | `id.resp_h`                 | The responder’s IP address.                                                             |
| `dst_endpoint.port`            | `id.resp_p`                 | The responder’s port number.                                                            |
| `dst_endpoint.agent_list[].name` | `server`                  | The server’s version string.                                                            |
| `client_hassh.fingerprint.value` | `hassh`                   | The hassh information.                                                                  |
| `server_hassh.fingerprint.value` | `hasshServer`             | The hasshServer information.                                                            |
| `count`                        | `auth_attempts`             | The number of authentication attempts observed.                                         |
| `protocol_ver`                 | `version`                   | SSH major version (1, 2, or unset).  (Use string value for vendor compatibility)        |

 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Evaluation Conditions | Zeek Field Description                                                                  |
| ------------------------------ | ----------------- | --------------------- | --------------------------------------------------------------------------------------- |
| `activity_id`                  | `auth_success`    | If "true" then "99", if "false" then "4", else "6". | Authentication result (true=success, false=failure, unset=unknown). |
| `activity_name`                | `auth_success`    | If "true" then "Authorization Successful", else defined by activity_id. | Authentication result (true=success, false=failure, unset=unknown). |
| `type_uid`                     | `auth_success`    | If "true" then "400799", if "false" then "400704", else "400706". | Authentication result (true=success, false=failure, unset=unknown). |
| `connection_info.direction_id` | `direction`       | If "INBOUND" then "1", if "OUTBOUND" then "2", else "3". |                                                      |
| `client_hassh.algorithm_id`    | `hassh`           | If `hassh` is present, MD5 (algorithm_id = "1") is used to derive it. | The hassh information.                  |
| `server_hassh.algorithm_id`    | `hasshServer`     | If `hasshServer` is present, MD5 (algorithm_id = "1") is used to derive it. | The hasshServer information.      |

 ### Unmapped (proposed):
| OCSF                     | Raw                | Zeek Field Description                                                                  |
| -------------------------| -------------------| --------------------------------------------------------------------------------------- |
| `unmapped`               | `hasshVersion`     | The hasshVersion information.                                                           |
| `unmapped`               | `hasshAlgorithms`  | The hasshAlgorithms information.                                                        |
| `unmapped`               | `hasshServerAlgorithms` | The hasshServerAlgorithms information.                                             |
| `unmapped`               | `cipher_alg`       | The encryption algorithm in use.                                                        |
| `unmapped`               | `compression_alg`  | The compression algorithm in use.                                                       |
| `unmapped`               | `host_key`         | The server’s key fingerprint.                                                           |
| `unmapped`               | `host_key_alg`     | The server host key’s algorithm.                                                        |
| `unmapped`               | `kex_alg`          | The key exchange algorithm in use.                                                      |
| `unmapped`               | `mac_alg`          | The signing (MAC) algorithm in use.                                                     |
| `unmapped`               | `cshka`            | The cshka information.                                                                  |
| `unmapped`               | `sshka`            | The sshka information.        
