# Event Dossier: Zeek conn.log
### Summary:
- **Description**: Translates a Zeek conn.log to OCSF. 

- **Event References**:
  - https://schema.ocsf.io/1.4.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/conn.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/conn/main.zeek.html#type-Conn::Info

 ### OCSF Version: v1.4.0
  
 ### Static value mapping
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.4.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4001         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |
| `connection_info.direction_id`      | 0            | Integer    |


 ### Direct field mapping:
| OCSF                          | Raw             | Zeek Field Description                                                                  | Notes                   |
| ----------------------------- | --------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                        | `ts`            | Time when the connection began.                                                         | Convert to epoch value. <br>Type is timestamp_t (Long). |
| `start_time`                  | `ts`            | Time when the connection began.                                                         | Convert to epoch value. <br>Type is timestamp_t (Long). |
| `metadata.logged_time`        | `_write_ts`     | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is timestamp_t (Long). |
| `metadata.loggers[].name`     | `_system_name`  | Name of the system or logging subsystem generating the log entry.                       |                         |
| `metadata.log_name`           | `_path`         | Log name.                                                                               |                         |
| `metadata.uid`                | `uid`           | Unique ID for the connection.                                                           |                         |
| `src_endpoint.ip`             | `id.orig_h`     | The originator’s IP address.                                                            | Type is ip_t.           |
| `src_endpoint.port`           | `id.orig_p`     | The originator’s port number.                                                           | Type is port_t (Integer). |
| `src_endpoint.location.country` | `orig_cc`     | Country code for GeoIP lookup of the originating IP address.                            |                         |
| `src_endpoint.mac`            | `orig_l2_addr`  | Link-layer address of the originator, if available.                                     | Type is mac_t.          |
| `dst_endpoint.ip`             | `id.resp_h`     | The responder’s IP address.                                                             | Type is ip_t.           |
| `dst_endpoint.port`           | `id.resp_p`     | The responder’s port number.                                                            | Type is port_t (Integer). |
| `dst_endpoint.location.country` | `resp_cc`     | Country code for GeoIP lookup of the responding IP address.                             | Type is mac_t.          |
| `dst_endpoint.mac`            | `resp_l2_addr`  | Link-layer address of the responder, if available.                                      |                         |
| `app_name`                    | `service`       | An identification of an application protocol being sent over the connection.            |                         |
| `connection_info.community_uid` | `community_id`| The community ID.                                                                       |                         |
| `connection_info.flag_history`  | `history`     | Records the state history of connections as a string of letters.                        |                         |
| `connection_info.protocol_name` | `proto`       | The transport layer protocol of the connection.                                         |                         |
| `duration`                    | `duration`      | How long the connection lasted.                                                         | Type is long_t.         |
| `status_code`                 | `conn_state`    | Possible connection states.                                                             | Type is string.         |
| `traffic.bytes_in`            | `resp_bytes`    | The number of payload bytes the responder sent.                                         | Type is long_t.         |
| `traffic.packets_in`          | `resp_pkts`     | Number of packets that the responder sent.                                              | Type is long_t.         |
| `traffic.bytes_out`           | `orig_bytes`    | The number of payload bytes the originator sent.                                        | Type is long_t.         |
| `traffic.packets_out`         | `orig_pkts`     | Number of packets that the originator sent.                                             | Type is long_t.         |
| `traffic.bytes_missed`        | `missed_bytes`  | Indicates the number of bytes missed in content gaps.                                   | Type is long_t.         |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                          | Raw                              | Zeek Field Description                                                       | Evaluation Conditions                                                                                     |
| ----------------------------- | -------------------------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `activity_id`                 | `conn_state` | Possible connection states. | If "SF" or "RSTO" or "RSTR" or "RSTRH" or "SH" or "SHR" then "2" (Close) <br>if "S0" then "4" (Fail), <br>if "REJ" then "5" (Refuse), <br>if "OTH" or "S1" or "S2" or "S3" then "6" (Traffic) <br>else "6" (Traffic) <br>Type is Integer. |
| `type_uid`                    | `class_uid` <br>+ `activity_id` | N/A | Calculate with: (`class_uid` * 100) + `activity_id` <br>Type is long_t. |
| `traffic.bytes`               | `resp_bytes` <br>+ `orig_bytes`  | The total number of payload bytes sent by both the originator and responder. | Sum of `resp_bytes` + `orig_bytes` <br>Type is long_t.       |
| `traffic.packets`             | `orig_pkts` <br>+ `resp_pkts`    | The total number of packets sent by both the originator and responder.       | Sum of `orig_pkts` + `resp_pkts` <br>Type is long_t.       |
| `observables[].value`         | `id.orig_h_name.vals`            | The set of names observed for a given originator address.                    | In a record where <br>`observables[].name` = "src_endpoint.hostname" <br>and `observables[].type_id` = "1" (Type is Integer) <br>and`observables[].reputation.provider` = `id.orig_h_name.src` <br>and`observables[].reputation.base_score` = "0.0" (Type is float_t) <br>and `observables[].reputation.score_id` = "0" (Type is Integer) |
| `observables[].value`         | `id.resp_h_name.vals`            | The set of names observed for a given responder address.                     | In a record where <br>`observables[].name` = "dst_endpoint.hostname" <br>and `observables[].type_id` = "1" (Type is Integer) <br>and`observables[].reputation.provider` = `id.resp_h_name.src` <br>and`observables[].reputation.base_score` = "0.0" (Type is float_t) <br>and `observables[].reputation.score_id` = "0" (Type is Integer) |


 ### Unmapped (proposed):

| OCSF                        | Raw              | Zeek Field Description                                                                  |
| --------------------------- | ---------------- | --------------------------------------------------------------------------------------- |
| `(network_endpoint).vlan_uid` | `vlan`           | The outer VLAN for this connection, if applicable.                                    |
| `unmapped`                  | `app`            |                                                                                         |
| `unmapped`                  | `tunnel_parents` | If this connection was over a tunnel, indicate the uid values for any encapsulating parent connections. |
| `unmapped`                  | `local_orig`     | Indicates if the connection is originated locally.                                      |
| `unmapped`                  | `local_resp`     | Indicates if the connection is responded to locally.                                    |
| `unmapped`                  | `orig_ip_bytes`  | Number of IP level bytes that the originator sent.                                      |
| `unmapped`                  | `resp_ip_bytes`  | Number of IP level bytes that the responder sent.                                       |
