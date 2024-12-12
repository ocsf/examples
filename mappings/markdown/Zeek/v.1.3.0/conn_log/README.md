# Event Dossier: Zeek conn.log
### Summary:
- **Description**: Translates a Zeek conn.log to OCSF. 

- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/conn.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/conn/main.zeek.html#type-Conn::Info

 ### OCSF Version: v1.3.0
  
 ### Static value mapping
| OCSF field                          | Value                                           |
| ----------------------------------- | ----------------------------------------------- |
| `metadata.version`                  | "1.3.0"                                         |
| `category_uid`                      | "4"                                             |
| `class_uid`                         | "4001"                                          |
| `severity_id`                       | "1"                                             |
| `metadata.product.name`             | "Zeek"                                          |
| `metadata.product.vendor_name`      | "Zeek"                                          |


 ### Direct field mapping:
| OCSF                          | Raw             | Zeek Field Description                                                                  |
| ----------------------------- | --------------- | --------------------------------------------------------------------------------------- |
| `time`                        | `ts`            | Time when the connection began.                                                         |
| `start_time`                  | `ts`            | Time when the connection began.                                                         |
| `metadata.logged_time`        | `_write_ts`     | Timestamp indicating when the log entry was written to disk.                            |
| `metadata.loggers[].name`     | `_system_name`  | Name of the system or logging subsystem generating the log entry.                       |
| `metadata.log_name`           | `_path`         | Log name.                                                                               |
| `metadata.uid`                | `uid`           | Unique ID for the connection.                                                           |
| `src_endpoint.ip`             | `id.orig_h`     | The originator’s IP address.                                                            |
| `src_endpoint.port`           | `id.orig_p`     | The originator’s port number.                                                           |
| `src_endpoint.location.country` | `orig_cc`     | Country code for GeoIP lookup of the originating IP address.                            |
| `src_endpoint.mac`            | `orig_l2_addr`  | Link-layer address of the originator, if available.                                     |
| `dst_endpoint.ip`             | `id.resp_h`     | The responder’s IP address.                                                             |
| `dst_endpoint.port`           | `id.resp_p`     | The responder’s port number.                                                            |
| `dst_endpoint.location.country` | `resp_cc`     | Country code for GeoIP lookup of the responding IP address.                             |
| `dst_endpoint.mac`            | `resp_l2_addr`  | Link-layer address of the responder, if available.                                      |
| `app_name`                    | `service`       | An identification of an application protocol being sent over the connection.            |
| `connection_info.community_uid` | `community_id`| The community ID.                                                                       |
| `connection_info.protocol_name` | `proto`       | The transport layer protocol of the connection.                                         |
| `duration`                    | `duration`      | How long the connection lasted.                                                         |
| `network_endpoint.vlan_uid`   | `vlan`          | The outer VLAN for this connection, if applicable.                                      |
| `status_code`                 | `conn_state`    | Possible connection states.                                                             |
| `traffic.bytes_in`            | `resp_bytes`    | The number of payload bytes the responder sent.                                         |
| `traffic.packets_in`          | `resp_pkts`     | Number of packets that the responder sent.                                              |
| `traffic.bytes_out`           | `orig_bytes`    | The number of payload bytes the originator sent.                                        |
| `traffic.packets_out`         | `orig_pkts`     | Number of packets that the originator sent.                                             |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                          | Raw                              | Evaluation Conditions                                                                                  | Zeek Field Description                                                                                   |
| ----------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| `traffic.bytes`               | `resp_bytes` + `orig_bytes`      | Sum of `resp_bytes` + `orig_bytes`                                                                     | The total number of payload bytes sent by both the originator and responder.                             |
| `traffic.packets`             | `orig_pkts` + `resp_pkts`        | Sum of `orig_pkts` + `resp_pkts`                                                                       | The total number of packets sent by both the originator and responder.                                    |
| `src_endpoint.observables[].value` | `id.orig_h_name.vals`         | In a record where `src_endpoint.observables[].reputation.provider` = `id.orig_h_name.src` AND `src_endpoint.observables[].type_id` = "1" AND `src_endpoint.observables[].type` = "Hostname" | The set of names observed for a given originator address. |
| `dst_endpoint.observables[].value` | `id.resp_h_name.vals`         | In a record where `dst_endpoint.observables[].reputation.provider` = `id.resp_h_name.src` AND `dst_endpoint.observables[].type_id` = "1" AND `dst_endpoint.observables[].type` = "Hostname" | The set of names observed for a given responder address. |

 ### Unmapped (proposed):

| OCSF                        | Raw              | Zeek Field Description                                                                 |
| --------------------------- | ---------------- | --------------------------------------------------------------------------------------- |
| `(bytes_missed)`            | `missed_bytes`   | Indicates the number of bytes missed in content gaps.                                   |
| `connection_info.(history)` | `history`        | Records the state history of connections as a string of letters.                        |
| `unmapped`                  | `app`            | (No description available)                                                              |
| `unmapped`                  | `corelight_shunted` | (No description available)                                                            |
| `unmapped`                  | `pcr`            | (No description available)                                                              |
| `unmapped`                  | `spcap.rule`     | (No description available)                                                              |
| `unmapped`                  | `spcap.trigger`  | (No description available)                                                              |
| `unmapped`                  | `spcap.url`      | (No description available)                                                              |
| `unmapped`                  | `suri_ids`       | (No description available)                                                              |
| `unmapped`                  | `tunnel_parents` | If this connection was over a tunnel, indicate the uid values for any encapsulating parent connections. |
| `unmapped`                  | `local_orig`     | Indicates if the connection is originated locally.                                      |
| `unmapped`                  | `local_resp`     | Indicates if the connection is responded to locally.                                    |
| `unmapped`                  | `orig_ip_bytes`  | Number of IP level bytes that the originator sent.                                      |
| `unmapped`                  | `resp_ip_bytes`  | Number of IP level bytes that the responder sent.                                       |
