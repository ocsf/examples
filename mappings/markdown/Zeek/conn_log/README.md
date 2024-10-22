# Event Dossier: Zeek conn.log
### Summary:
- **Description**: Translates a Zeek conn.log to OCSF. 

- **Event References**:
  - https://docs.zeek.org/en/master/logs/conn.html
  - https://schema.ocsf.io/1.3.0/classes/network_activity
 
 ### Static mapping: OCSF Version 1.3.0
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4001`
 - `class_name`: `Network Activity`
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
|`app_name`                     |`service`      |
|`connection_info.protocol_name`|`proto`        |
|`duration`                     |`duration`     |
|`traffic.bytes_in`             |`resp_bytes`   |
|`traffic.packets_in`           |`resp_pkts`    |
|`traffic.bytes_out`            |`orig_bytes`   |
|`traffic.packets_out`          |`orig_pkts`    |
|`traffic.bytes`                |`resp_bytes` + `orig_bytes` |
|`traffic.packets`              |`orig_pkts` + `resp_pkts`   |



 ### Unmapped (proposed) New OCSF attributes:

| OCSF                 | Raw             |
| ---------------------| ----------------| 
|`(bytes_missed)`        |`missed_bytes` |
|`(connection_history)`  |`history`      |
|`unmapped`              |`conn_state`   |
