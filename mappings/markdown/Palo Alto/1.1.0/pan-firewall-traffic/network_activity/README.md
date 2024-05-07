# Event Dossier: Pan Firewall Traffic to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `paloalto`
* Product name: `pan-firewall-traffic`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION is null then 0 WHEN ACTION = 'allow' then 1 WHEN ACTION = 'deny' then 2 WHEN ACTION = 'drop' then 2 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION is null then 0 WHEN ACTION = 'allow' then 1 WHEN ACTION = 'deny' then 2 WHEN ACTION = 'drop' then 2 ELSE 99 END``` |
| activity_id | ```CASE WHEN TYPE is null then 0 WHEN TYPE = 'TRAFFIC' then 6 ELSE 99 END``` |
| activity_name | ```CASE (CASE WHEN TYPE is null then 0 WHEN TYPE = 'TRAFFIC' then 6 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```SOURCE_USER::VARCHAR``` |
| app_name | ```APPLICATION::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```PROTOCOL::VARCHAR``` |
| connection_info.protocol_num | ```CASE WHEN PROTOCOL = 'tcp' THEN 6 WHEN PROTOCOL = 'udp' THEN 17 WHEN PROTOCOL = 'icmp' THEN 1 ELSE -1 END``` |
| connection_info.session.expiration_reason | ```SESSION_END_REASON::VARCHAR``` |
| connection_info.session.uid | ```SESSION_ID::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| dst_endpoint.intermediate_ips | ```ARRAY_CONSTRUCT(NAT_DESTINATION_IP::VARCHAR)``` |
| dst_endpoint.ip | ```DESTINATION_ADDRESS::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT::VARCHAR``` |
| dst_endpoint.zone | ```DESTINATION_ZONE::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', TRY_TO_TIMESTAMP_LTZ(RECEIVE_TIME,'yyyy/mm/dd hh24:mi:ss')::TIMESTAMP_LTZ)``` |
| end_time_dt | ```TRY_TO_TIMESTAMP_LTZ(RECEIVE_TIME,'yyyy/mm/dd hh24:mi:ss')::TIMESTAMP_LTZ``` |
| firewall_rule.category | ```CATEGORY::VARCHAR``` |
| firewall_rule.name | ```RULE_NAME::VARCHAR``` |
| firewall_rule.uid | ```RULE_UUID::VARCHAR``` |
| metadata.product.name | ```'pan-firewall-traffic'``` |
| metadata.product.vendor_name | ```'paloalto'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.intermediate_ips | ```ARRAY_CONSTRUCT(NAT_SOURCE_IP::VARCHAR)``` |
| src_endpoint.ip | ```SOURCE_ADDRESS::VARCHAR``` |
| src_endpoint.port | ```SOURCE_PORT::VARCHAR``` |
| src_endpoint.zone | ```SOURCE_ZONE::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', START_TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```START_TIME::TIMESTAMP_LTZ``` |
| time | ```date_part('epoch_milliseconds', generated_time::TIMESTAMP_LTZ)``` |
| time_dt | ```generated_time::TIMESTAMP_LTZ``` |
| traffic.bytes | ```BYTES::NUMBER``` |
| traffic.bytes_in | ```BYTES_RECEIVED::NUMBER``` |
| traffic.bytes_out | ```BYTES_SENT::NUMBER``` |
| traffic.chunks | ```SCTP_CHUNKS::NUMBER``` |
| traffic.chunks_in | ```SCTP_CHUNKS_RECEIVED::NUMBER``` |
| traffic.chunks_out | ```SCTP_CHUNKS_SENT::NUMBER``` |
| traffic.packets | ```PACKETS::NUMBER``` |
| traffic.packets_in | ```PACKETS_RECEIVED::NUMBER``` |
| traffic.packets_out | ```PACKETS_SENT::NUMBER``` |
| type_name | ```CASE (CASE WHEN ACTION is null then 400100 WHEN ACTION = 'allow' then 400101 WHEN ACTION = 'deny' then 400102 WHEN ACTION = 'drop' then 400102 ELSE 400199 END) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```CASE WHEN ACTION is null then 400100 WHEN ACTION = 'allow' then 400101 WHEN ACTION = 'deny' then 400102 WHEN ACTION = 'drop' then 400102 ELSE 400199 END``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
