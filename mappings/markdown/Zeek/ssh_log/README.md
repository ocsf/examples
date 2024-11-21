# Event Dossier: Zeek ssh.log
### Summary:
- **Description**: Translates a Zeek ssh.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/ssh_activity
  - https://docs.zeek.org/en/master/logs/ssh.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssh/main.zeek.html#type-SSH::Info
    
 ### Static mapping: OCSF Version 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `SSH Activity`
 - `class_uid`: `4007`
 - `metadata.log_name`: `ssh.log`
 - `metadata.loggers[].log_provider`: `Zeek`
 - `metadata.loggers[].product.name`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `ssh.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/ssh.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`
 - `dst_endpoint.agent_list[].type`: `Remote Access`
 - `dst_endpoint.agent_list[].type_id`: `9`
 - `src_endpoint.agent_list[].type`: `Remote Access`
 - `src_endpoint.agent_list[].type_id`: `9`

 ### Mapping:

| OCSF                           | Raw                         | Zeek Field Description                                                                 |
| ------------------------------ | --------------------------- | --------------------------------------------------------------------------------------- |
| `time`                         | `ts`                        | Timestamp indicating when the event occurred.                                           |
| `start_time`                   | `ts`                        | Timestamp indicating when the event occurred.                                           |
| `metadata.logged_time`         | `_write_ts`                 | Timestamp indicating when the log entry was written to disk.                            |
| `metadata.loggers[].name`      | `_system_name`              | Name of the system or logging subsystem generating the log entry.                        |
| `metadata.uid`                 | `uid`                       | Unique ID for the connection.                                                           |
| `src_endpoint.ip`              | `id.orig_h`                 | The originator’s IP address.                                                            |
| `src_endpoint.port`            | `id.orig_p`                 | The originator’s port number.                                                           |
| `src_endpoint.agent_list[].name` | `client`                    | The client’s version string.                                                            |
| `src_endpoint.location.city`   | `remote_location.city`      | The city.                                                                               |
| `src_endpoint.location.country`| `remote_location.country_code` | The country code.                                                                    |
| `src_endpoint.location.lat`    | `remote_location.latitude`  | Latitude.                                                                               |
| `src_endpoint.location.long`   | `remote_location.longitude` | Longitude.                                                                              |
| `src_endpoint.location.region` | `remote_location.region`    | The region.                                                                             |
| `dst_endpoint.ip`              | `id.resp_h`                 | The responder’s IP address.                                                             |
| `dst_endpoint.port`            | `id.resp_p`                 | The responder’s port number.                                                            |
| `dst_endpoint.agent_list[].name` | `server`                    | The server’s version string.                                                            |
| `client_hassh.algorithm`       | `hasshAlgorithms`           | The hasshAlgorithms information.                                                        |
| `client_hassh.fingerprint`     | `hassh`                     | The hassh information.                                                                  |
| `server_hassh.algorithm`       | `hasshServerAlgorithms`     | The hasshServerAlgorithms information.                                                  |
| `server_hassh.fingerprint`     | `hasshServer`               | The hasshServer information.                                                            |
| `count`                        | `auth_attempts`             | The number of authentication attempts observed.                                         |
| `connection_info.direction`    | `direction`                 | Direction of the connection (INBOUND/OUTBOUND).                                         |
| `protocol_ver`                 | `version`                   | SSH major version (1, 2, or unset).                                                     |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Evaluation Conditions | Zeek Field Description                                                                  |
| ------------------------------ | ----------------- | --------------------- | --------------------------------------------------------------------------------------- |
| `activity_id`                  | `auth_success`    | Change `activity_id` value based on mapped `auth_success` value. | Authentication result (T=success, F=failure, unset=unknown).                          |


 ### Unmapped (proposed):
| OCSF                     | Raw                | Zeek Field Description                                                                 |
| -------------------------| -------------------| --------------------------------------------------------------------------------------- |
| `unmapped`               | `inferences`       | Inferences from SOL analysis.                                                           |
| `unmapped`               | `hasshVersion`     | The hasshVersion information.                                                           |
| `unmapped`               | `cipher_alg`       | The encryption algorithm in use.                                                        |
| `unmapped`               | `compression_alg`  | The compression algorithm in use.                                                       |
| `unmapped`               | `host_key`         | The server’s key fingerprint.                                                           |
| `unmapped`               | `host_key_alg`     | The server host key’s algorithm.                                                        |
| `unmapped`               | `kex_alg`          | The key exchange algorithm in use.                                                      |
| `unmapped`               | `mac_alg`          | The signing (MAC) algorithm in use.                                                     |
| `unmapped`               | `cshka`            | The cshka information.                                                                  |
| `unmapped`               | `sshka`            | The sshka information.        
