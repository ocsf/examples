# Event Dossier: Zeek ssh.log
### 
- **Description**: Translates a Zeek ssh.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/ssh_activity
  - https://docs.zeek.org/en/master/logs/ssh.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssh/main.zeek.html#type-SSH::Info
    
 ### OCSF Version: 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `SSH Activity`
 - `class_uid`: `4007`
 - `metadata.log_name`: `ssh.log`
 - `metadata.loggers.log_provider`: `Zeek`
 - `metadata.loggers.product.name=`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `ssh.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/ssh.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`
 - `dst_endpoint.agent_list.type`: `Remote Access`
 - `dst_endpoint.agent_list.type_id`: `9`
 - `src_endpoint.agent_list.type`: `Remote Access`
 - `src_endpoint.agent_list.type_id`: `9`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                           | Raw               |
| ------------------------------ | ----------------- |
|`time`                          |`ts`               |
|`start_time`                    |`ts`               |
|`metadata.loggers.logged_time`  |`_write_ts`        |
|`metadata.loggers.name`         |`_system_name`     |
|`metadata.uid`                  |`uid`              |
|`src_endpoint.ip`               |`id.orig_h`        |
|`src_endpoint.port`             |`id.orig_p`        |
|`src_endpoint.agent_list.name`  |`client`           |   
|`src_endpoint.location.city`    |`remote_location.city`        |
|`src_endpoint.location.country` |`remote_location.country_code`|
|`src_endpoint.location.lat`     |`remote_location.latitude`    |
|`src_endpoint.location.long`    |`remote_location.longitude`   | 
|`src_endpoint.location.region`  |`remote_location.region`      |
|`dst_endpoint.ip`               |`id.resp_h`        |
|`dst_endpoint.port`             |`id.resp_p`        |
|`dst_endpoint.agent_list.name`  |`server`           |
|`client_hassh.algorithm`        |`hasshAlgorithms`  |
|`client_hassh.fingerprint`      |`hassh`            |
|`server_hassh.algorithm`        |`hasshServerAlgorithms`    |
|`server_hassh.fingerprint`      |`hasshServer`      |
|`count`                         |`auth_attempts`    |
|`network_activity.connection_info.direction` |`direction` |
|`protocol_ver`                  |`version`          |
|`activity_id:4`                 |`auth_success`     |

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                          | Raw               | Notes              |
| ------------------------------| ------------------| -- ----------------|


 ### Proposed New OCSF attributes:
 - 
| OCSF                     | Raw                      |
| -------------------------| -------------------------|
|`unmapped`                      |`inferences`    |
|`unmapped`                      |`hasshVersion`    |
|`unmapped`                      |`cipher_alg`    |
|`unmapped`                      |`compression_alg`    |
|`unmapped`                      |`host_key`    |
|`unmapped`                      |`host_key_alg`    |
|`unmapped`                      |`kex_alg`    |
|`unmapped`                      |`mac_alg`    |
|`unmapped`                      |`cshka`    |
|`unmapped`                      |`sshka`    |
