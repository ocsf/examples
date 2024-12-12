# Event Dossier: Zeek ssh.log
### Summary:
- **Description**: Translates a Zeek ssh.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/ssh_activity
  - https://docs.zeek.org/en/master/logs/ssh.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssh/main.zeek.html#type-SSH::Info


 ### OCSF Version: v1.3.0


 ### Static value mapping:
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.3.0"      |            |
| `category_uid`                      | "4"          | Integer    |
| `class_uid`                         | "4007"       | Integer    |
| `severity_id`                       | "1"          | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |
| `dst_endpoint.agent_list[].name`    | "SSH Server" |            |
| `dst_endpoint.agent_list[].type_id` | "9"          | Integer    |
| `src_endpoint.agent_list[].name`    | "SSH Client" |            |
| `src_endpoint.agent_list[].type_id` | "9"          | Integer    |


 ### Direct field mapping:
| OCSF                           | Raw                         | Zeek Field Description                                                                  | Notes                   |
| ------------------------------ | --------------------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                         | `ts`                        | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `start_time`                   | `ts`                        | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `metadata.logged_time`         | `_write_ts`                 | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is Integer. |
| `metadata.loggers[].name`      | `_system_name`              | Name of the system or logging subsystem generating the log entry.                       |                         |
| `metadata.log_name`            | `_path`                     | Log name.                                                                               |                         |
| `metadata.uid`                 | `uid`                       | Unique ID for the connection.                                                           |                         |
| `src_endpoint.ip`              | `id.orig_h`                 | The originator’s IP address.                                                            |                         |
| `src_endpoint.port`            | `id.orig_p`                 | The originator’s port number.                                                           | Integer                 |
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
| `count`                        | `auth_attempts`             | The number of authentication attempts observed.                                         | Integer                 |
| `protocol_ver`                 | `version`                   | SSH major version (1, 2, or unset).                                                     | As string for vendor compatibility. |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Zeek Field Description                                              | Evaluation Conditions                                                                   |
| ------------------------------ | ----------------- | ------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `activity_id`                  | `auth_success`    | Authentication result.                                              | If "true" then "99", <br>if "false" then "4", <br>else "6". <br>Type is Integer.        |
| `activity_name`                | `auth_success`    | Authentication result.                                              | If "true" then "Authorization Successful", <br>else defined by activity_id.             |
| `type_uid`                     | `auth_success`    | Authentication result.                                              | If "true" then "400799", <br>if "false" then "400704", <br>else "400706". <br>Type is Integer. |
| `connection_info.direction_id` | `direction`       | Direction of the connection. If the client was a local host logging into an external host, this would be OUTBOUND. INBOUND would be set for the opposite situation. | If "INBOUND" then "1", <br>if "OUTBOUND" then "2", <br>else "3". |
| `client_hassh.fingerprint.algorithm_id` | `hassh`  | The hassh information.                                              | If `hassh` is present, then "1". (MD5) <br>Type is Integer.                             |
| `server_hassh.fingerprint.algorithm_id` | `hasshServer` | The hasshServer information.                                   | If `hasshServer` is present, then "1". (MD5) <br>Type is Integer.                       |
| `observables[].value`          | `hasshVersion`    | The hasshVersion information.                                       | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "hassh Version"               |
| `observables[].value`          | `hasshAlgorithms` | The hasshAlgorithms information.                                    | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "hassh Algorithms"            |
| `observables[].value`          | `hasshServerAlgorithms` | The hasshServerAlgorithms information.                        | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "hasshServerAlgorithms"       |
| `observables[].value`          | `cipher_alg`      | The encryption algorithm in use.                                    | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "Encryption algorithm"        |
| `observables[].value`          | `compression_alg` | The compression algorithm in use.                                   | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "Compression algorithm"       |
| `observables[].value`          | `host_key`        | The server’s key fingerprint.                                       | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "Server’s key fingerprint"    |
| `observables[].value`          | `host_key_alg`    | The server host key’s algorithm.                                    | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "Server host key’s algorithm" |
| `observables[].value`          | `kex_alg`         | The key exchange algorithm in use.                                  | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "Key exchange algorithm"      |
| `observables[].value`          | `mac_alg`         | The signing (MAC) algorithm in use.                                 | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "Signing (MAC) algorithm"     |
| `observables[].value`          | `cshka`           | The cshka information.                                              | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "cshka"                       |
| `observables[].value`          | `sshka`           | The sshka information.                                              | In an record where <br>`observables[].type_id` = "99" <br>and `observables[].name` = "sshka"                       |
