# Event Dossier: Zeek Conn Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `zeek`
* Product name: `zeek-conn-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN CONN_STATE is NULL THEN 0 WHEN CONN_STATE ILIKE '%%Connection established%%' THEN 1 WHEN CONN_STATE ILIKE '%%Connection attempt rejected%%'    THEN 2 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN CONN_STATE is NULL THEN 0 WHEN CONN_STATE ILIKE '%%Connection established%%' THEN 1 WHEN CONN_STATE ILIKE '%%Connection attempt rejected%%'    THEN 2 ELSE 99 END``` |
| activity_id | ```0::NUMBER``` |
| activity_name | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| api.service.name | ```SERVICE::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```PROTO::VARCHAR``` |
| connection_info.protocol_num | ```CASE WHEN proto = 'tcp' THEN 6 WHEN proto = 'udp' THEN 17 WHEN proto = 'icmp' THEN 1 ELSE -1 END``` |
| connection_info.uid | ```UID::VARCHAR``` |
| dst_endpoint.ip | ```RESPONDER_HOST::VARCHAR``` |
| dst_endpoint.port | ```RESPONDER_PORT::VARCHAR``` |
| duration | ```(DURATION*1000)::NUMBER``` |
| metadata.product.name | ```'zeek-conn-logs'``` |
| metadata.product.vendor_name | ```'zeek'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```ORIGINATOR_HOST::VARCHAR``` |
| src_endpoint.port | ```RESPONDER_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', ts::TIMESTAMP_LTZ)``` |
| time_dt | ```ts::TIMESTAMP_LTZ``` |
| traffic.bytes_in | ```RESPONDER_BYTES::NUMBER``` |
| traffic.bytes_out | ```ORIGINATOR_BYTES::NUMBER``` |
| traffic.packets_in | ```RESPONDER_PACKETS::NUMBER``` |
| traffic.packets_out | ```ORIGINATOR_PACKETS::NUMBER``` |
| type_name | ```CASE ('400100'::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```'400100'::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
