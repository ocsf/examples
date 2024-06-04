# Event Dossier: Oracle Service Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `oracle`
* Product name: `oracle-service-logs`
* Event codes: `contains(EVENT_TYPE ,'com.oraclecloud.networkfirewall') OR contains(EVENT_TYPE ,'com.oraclecloud.vcn.flowlogs')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION = 'ACCEPT' THEN 1 WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'REJECT' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION = 'ACCEPT' THEN 1 WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'REJECT' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```0::NUMBER``` |
| activity_name | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| cloud.provider | ```'Oracle'::VARCHAR``` |
| connection_info.protocol_name | ```LOWER(COALESCE(PROTOCOL_NAME, RAW:data:proto))::VARCHAR``` |
| connection_info.protocol_num | ```PROTOCOL::NUMBER``` |
| dst_endpoint.ip | ```COALESCE(DESTINATION_ADDRESS, RAW:data:dst)::VARCHAR``` |
| dst_endpoint.port | ```COALESCE(DESTINATION_PORT, RAW:data:dport)::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', END_TIME::TIMESTAMP_LTZ)``` |
| end_time_dt | ```END_TIME::TIMESTAMP_LTZ``` |
| firewall_rule.name | ```RAW:data:rule::VARCHAR``` |
| firewall_rule.uid | ```RAW:data:rule_uuid::VARCHAR``` |
| metadata.event_code | ```EVENT_TYPE``` |
| metadata.product.name | ```'oracle-service-logs'``` |
| metadata.product.vendor_name | ```'oracle'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN RAW:data:severity IS NULL THEN 0 WHEN RAW:data:severity = 'medium' THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN RAW:data:severity IS NULL THEN 0 WHEN RAW:data:severity = 'medium' THEN 3 ELSE 99 END::NUMBER``` |
| src_endpoint.ip | ```COALESCE(SOURCE_ADDRESS, RAW:data:src)::VARCHAR``` |
| src_endpoint.port | ```COALESCE(SOURCE_PORT, RAW:data:sport)::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', START_TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```START_TIME::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN STATUS IS NULL THEN 0 WHEN STATUS = 'OK' THEN 1 WHEN STATUS = 'SKIPDATA' THEN 2 ELSE 99 END::NUMBER::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS IS NULL THEN 0 WHEN STATUS = 'OK' THEN 1 WHEN STATUS = 'SKIPDATA' THEN 2 ELSE 99 END::NUMBER::NUMBER``` |
| time | ```date_part('epoch_milliseconds', time::TIMESTAMP_LTZ)``` |
| time_dt | ```time::TIMESTAMP_LTZ``` |
| traffic.bytes_out | ```BYTES_OUT::NUMBER``` |
| traffic.packets | ```PACKETS::NUMBER``` |
| type_name | ```CASE (400100::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```400100::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
