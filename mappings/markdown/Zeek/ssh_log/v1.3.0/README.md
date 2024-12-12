# Event Dossier: Zeek ssh.log
### Summary:
- **Description**: Translates a Zeek ssh.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/ssh_activity
  - https://docs.zeek.org/en/master/logs/ssh.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssh/main.zeek.html#type-SSH::Info
    
 ### OCSF Version: v1.3.0

 ### Static value mapping:
| OCSF field                          | Value                                           |
| ----------------------------------- | ----------------------------------------------- |
| `metadata.version`                  | "1.3.0"                                         |
| `category_uid`                      | "4"                                             |
| `class_uid`                         | "4007"                                          |
| `severity_id`                       | "1"                                             |
| `metadata.log_name`                 | "ssh.log"                                       |
| `metadata.product.name`             | "Zeek"                                          |
| `metadata.product.vendor_name`      | "Zeek"                                          |
| `dst_endpoint.agent_list[].name`    | "SSH Server"                                    |
| `dst_endpoint.agent_list[].type_id` | "9"                                             |
| `src_endpoint.agent_list[].name`    | "SSH Client"                                    |
| `src_endpoint.agent_list[].type_id` | "9"                                             |

 ### Direct field mapping:
| OCSF                           | Raw                         | Zeek Field Description                                                                  | Notes                   |
| ------------------------------ | --------------------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                         | `ts`                        | Timestamp indicating when the event occurred.                                           | Convert to epoch value. |
| `start_time`                   | `ts`                        | Timestamp indicating when the event occurred.                                           | Convert to epoch value. |
| `metadata.logged_time`         | `_write_ts`                 | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. |
| `metadata.loggers[].name`      | `_system_name`              | Name of the system or logging subsystem generating the log entry.                       |                         |
| `metadata.uid`                 | `uid`                       | Unique ID for the connection.                                                           |                         |
| `src_endpoint.ip`              | `id.orig_h`                 | The originator’s IP address.                                                            |                         |
| `src_endpoint.port`            | `id.orig_p`                 | The originator’s port number.                                                           |                         |
| `src_endpoint.agent_list[].name` | `client`                  | The client’s version string.                                                            |                         |
| `src_endpoint.location.city`   | `remote_location.city`      | The city.                                                                               |                         |
| `src_endpoint.location.country`| `remote_location.country_code` | The country code.                                                                    |                         |
| `src_endpoint.location.lat`    | `remote_location.latitude`  | Latitude.                                                                               |                         |
| `src_endpoint.location.long`   | `remote_location.longitude` | Longitude.                                                                              |                         |
| `src_endpoint.location.region` | `remote_location.region`    | The region.                                                                             |                         |
| `dst_endpoint.ip`              | `id.resp_h`                 | The responder’s IP address.                                                             |                         |
| `dst_endpoint.port`            | `id.resp_p`                 | The responder’s port number.                                                            |                         |
| `dst_endpoint.agent_list[].name` | `server`                  | The server’s version string.                                                            |                         |
| `client_hassh.fingerprint.value` | `hassh`                   | The hassh information.                                                                  |                         |
| `server_hassh.fingerprint.value` | `hasshServer`             | The hasshServer information.                                                            |                         |
| `count`                        | `auth_attempts`             | The number of authentication attempts observed.                                         |                         |
| `protocol_ver`                 | `version`                   | SSH major version (1, 2, or unset).                                                     | As string for vendor compatibility. |

 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Zeek Field Description                                              | Evaluation Conditions                                                                   |
| ------------------------------ | ----------------- | ------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `activity_id`                  | `auth_success`    | Authentication result (true=success, false=failure, unset=unknown). | If "true" then "99", if "false" then "4", else "6".                                     |
| `activity_name`                | `auth_success`    | Authentication result (true=success, false=failure, unset=unknown). | If "true" then "Authorization Successful", else defined by activity_id.                 |
| `type_uid`                     | `auth_success`    | Authentication result (true=success, false=failure, unset=unknown). | If "true" then "400799", if "false" then "400704", else "400706".                       |
| `connection_info.direction_id` | `direction`       |                                                                     | If "INBOUND" then "1", if "OUTBOUND" then "2", else "3".                                |
| `client_hassh.algorithm_id`    | `hassh`           | The hassh information.                                              | If `hassh` is present, MD5 (algorithm_id = "1") is used to derive it.                   |
| `server_hassh.algorithm_id`    | `hasshServer`     | The hasshServer information.                                        | If `hasshServer` is present, MD5 (algorithm_id = "1") is used to derive it.             |
| `observables[].value`          | `hasshVersion`    | The hasshVersion information.                                       | In an object where `observables[].type_id` = "99" and `observables[].type` = "hassh Version"               |
| `observables[].value`          | `hasshAlgorithms` | The hasshAlgorithms information.                                    | In an object where `observables[].type_id` = "99" and `observables[].type` = "hassh Algorithms"            |
| `observables[].value`          | `hasshServerAlgorithms` | The hasshServerAlgorithms information.                        | In an object where `observables[].type_id` = "99" and `observables[].type` = "hasshServerAlgorithms"       |
| `observables[].value`          | `cipher_alg`      | The encryption algorithm in use.                                    | In an object where `observables[].type_id` = "99" and `observables[].type` = "Encryption algorithm"        |
| `observables[].value`          | `compression_alg` | The compression algorithm in use.                                   | In an object where `observables[].type_id` = "99" and `observables[].type` = "Compression algorithm"       |
| `observables[].value`          | `host_key`        | The server’s key fingerprint.                                       | In an object where `observables[].type_id` = "99" and `observables[].type` = "Server’s key fingerprint"    |
| `observables[].value`          | `host_key_alg`    | The server host key’s algorithm.                                    | In an object where `observables[].type_id` = "99" and `observables[].type` = "Server host key’s algorithm" |
| `observables[].value`          | `kex_alg`         | The key exchange algorithm in use.                                  | In an object where `observables[].type_id` = "99" and `observables[].type` = "Key exchange algorithm"      |
| `observables[].value`          | `mac_alg`         | The signing (MAC) algorithm in use.                                 | In an object where `observables[].type_id` = "99" and `observables[].type` = "Signing (MAC) algorithm"     |
| `observables[].value`          | `cshka`           | The cshka information.                                              | In an object where `observables[].type_id` = "99" and `observables[].type` = "cshka"                       |
| `observables[].value`          | `sshka`           | The sshka information.                                              | In an object where `observables[].type_id` = "99" and `observables[].type` = "sshka"                       |
