# Event Dossier: Zeek conn.log
### Summary:
- **Description**: Translates a Zeek conn.log to OCSF. 

- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/conn.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/conn/main.zeek.html#type-Conn::Info
 
 ### Static mapping: OCSF Version 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `Network Activity`
 - `class_uid`: `4001`
 - `metadata.log_name`: `conn.log`
 - `metadata.loggers[].log_provider`: `Zeek`
 - `metadata.loggers[].product.name`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `conn.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/conn.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:

| OCSF                          | Raw           |
| ----------------------------- | --------------|
|`time`                         |`ts`           |
|`metadata.uid`                 |`uid`          |
|`src_endpoint.ip`              |`id.orig_h`    |
|`src_endpoint.port`            |`id.orig_p`    |
|`src_endpoint.location.country`|`orig_cc`      |
|`src_endpoint.mac`             |`orig_l2_addr` |
|`dst_endpoint.ip`              |`id.resp_h`    |
|`dst_endpoint.port`            |`id.resp_p`    |
|`dst_endpoint.location.country`|`resp_cc`      |
|`dst_endpoint.mac`             |`resp_l2_addr` |
|`app_name`                     |`service`      |
|`connection_info.community_uid`|`community_id` |
|`connection_info.protocol_name`|`proto`        |
|`duration`                     |`duration`     |
|`network_endpoint.vlan_uid`    |`vlan`         |
|`status_code`                  |`conn_state`   |
|`traffic.bytes_in`             |`resp_bytes`   |
|`traffic.packets_in`           |`resp_pkts`    |
|`traffic.bytes_out`            |`orig_bytes`   |
|`traffic.packets_out`          |`orig_pkts`    |
|`traffic.bytes`                |`resp_bytes` + `orig_bytes` |
|`traffic.packets`              |`orig_pkts` + `resp_pkts`   |

 ### Unmapped (proposed):

| OCSF                 | Raw             |
| ---------------------| ----------------| 
|`src_endpoint.observables.type_id:1 && src_endpoint.observables.reputation = id.orig_h_name.src` |`id.orig_h_name.vals` |
|`dst_endpoint.observables.type_id:1 && dst_endpoint.observables.reputation = id.orig_h_name.src` |`id.orig_h_name.vals` |
|`(bytes_missed)`        |`missed_bytes` |
|`(connection_info.history)`  |`history`      |
|`unmapped`                   |`app`          |
|`unmapped`                   |`corelight_shunted`   |
|`unmapped`                   |`pcr`          |
|`unmapped`                   |`spcap.rule`   |
|`unmapped`                   |`spcap.trigger`|
|`unmapped`                   |`spcap.url`    |
|`unmapped`                   |`suri_ids`     |
|`unmapped`                   |`tunnel_parents`|
|`unmapped`                   |`local_orig`   |
|`unmapped`                   |`local_resp`   |
|`unmapped`                   |`orig_ip_bytes`|
|`unmapped`                   |`resp_ip_bytes`|
