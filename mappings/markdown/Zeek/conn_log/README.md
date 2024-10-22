# Event Dossier: Zeek conn.log
### 
- **Description**: Translates a Zeek conn.log to OCSF. 

- **Event References**:
  - https://docs.zeek.org/en/master/logs/conn.html
  - https://schema.ocsf.io/1.0.0-rc.3/classes/network_activity
 
 ### OCSF Version: 1.0.0-rc.3
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4001`
 - `class_name`: `Network Activity`
 - `metadata.profiles`: `[security_control]`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.feature.name`: `conn.log`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:

| OCSF                          | Raw           |
| ----------------------------- | --------------|
|`time`                         |`ts`           |
|`uuid`                         |`uid`          |
|`src_endpoint.ip`              |`id.orig_h`    |
|`src_endpoint.port`            |`id.orig_p`    |
|`dst_endpoint.ip`              |`id.resp_h`    |
|`dst_endpoint.port`            |`id.resp_p`    |
|`connection_info.protocol_name`|`proto`        |
|`bytes_in`                     |`orig_bytes`   |
|`packets_in`                   |`orig_pkts`    |
|`orig_bytes.ip`                |`orig_ip_bytes`|
|`bytes_out`                    |`resp_bytes`   |
|`packets_out`                  |`resp_pkts`    |
|`resp_bytes.ip`                |`resp_ip_bytes`|
|`duration`                     |`duration`     |
|`unmapped`                     |`conn_state`   |


 ### Proposed New OCSF attributes:

| OCSF                 | Raw             |
| ---------------------| ----------------| 
|`application_protocol`|`service`        |
|`bytes_missed`        |`missed_bytes`   |
|`connection_history`  |`history`        |
