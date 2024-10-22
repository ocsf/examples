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
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                          | Raw           |
| ----------------------------- | --------------|
|`time`                         |`ts`           |
|`uuid`                         |`uid`          |
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

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.
| OCSF                 | Raw             | Notes                       |
| ---------------------| ----------------| ----------------------------|


 ### Proposed New OCSF attributes:
 - 
| OCSF                 | Raw             | Notes                       |
| ---------------------| ----------------| ----------------------------|
|`application_protocol`|`service`        |`propose new ocsf field name`|
|`bytes_missed`        |`missed_bytes`   |`propose new ocsf field name`|
|`connection_history`  |`history`        |`propose new ocsf field name`|
