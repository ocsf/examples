# Event Dossier: Checkpoint Traffic to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `checkpoint`
* Product name: `checkpoint-traffic`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION='Allow' THEN 1 WHEN ACTION='Accept' THEN 1 WHEN ACTION='Block' THEN 2 WHEN ACTION='Reject' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION='Allow' THEN 1 WHEN ACTION='Accept' THEN 1 WHEN ACTION='Block' THEN 2 WHEN ACTION='Reject' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```2::NUMBER``` |
| activity_name | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.uid | ```RAW:loguid::VARCHAR``` |
| actor.session.created_time | ```date_part('epoch_milliseconds', BROWSE_TIME::TIMESTAMP_LTZ)``` |
| actor.session.created_time_dt | ```BROWSE_TIME::TIMESTAMP_LTZ``` |
| actor.session.uid | ```RAW:session_uid::VARCHAR``` |
| actor.user.domain | ```RAW:Domain::VARCHAR``` |
| actor.user.name | ```COALESCE(USER, RAW:src_user_name)::VARCHAR``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.direction | ```CASE (CASE WHEN RAW:ifdir='inbound' THEN 1 WHEN RAW:ifdir='outbound' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```CASE WHEN RAW:ifdir='inbound' THEN 1 WHEN RAW:ifdir='outbound' THEN 2 ELSE 99 END::NUMBER``` |
| connection_info.protocol_num | ```PROTO::NUMBER``` |
| connection_info.session.expiration_time | ```date_part('epoch_milliseconds', RAW:expire_time::TIMESTAMP_LTZ)``` |
| connection_info.session.expiration_time_dt | ```RAW:expire_time::TIMESTAMP_LTZ``` |
| device.interface_name | ```RAW:ifname::VARCHAR``` |
| device.ip | ```ORIGIN::VARCHAR``` |
| device.name | ```ORIGIN_SIC_NAME::VARCHAR``` |
| dst_endpoint.domain | ```CASE WHEN PARSE_URL(RESOURCE,1):host::VARCHAR REGEXP '^[a-zA-Z0-9-]+(\\\ .[a-zA-Z0-9-]+){1,}$' THEN PARSE_URL(RESOURCE,1):host::VARCHAR ELSE NULL END::VARCHAR``` |
| dst_endpoint.hostname | ```DST_MACHINE_NAME::VARCHAR``` |
| dst_endpoint.ip | ```DST::VARCHAR``` |
| dst_endpoint.port | ```SERVICE::VARCHAR``` |
| dst_endpoint.zone | ```RAW:outzone::VARCHAR``` |
| firewall_rule.category | ```RAW:rule_action::VARCHAR``` |
| firewall_rule.name | ```RULE_NAME::VARCHAR``` |
| firewall_rule.uid | ```RAW:rule_uid::VARCHAR``` |
| message | ```COALESCE(RAW:message_info, RAW:decision)::VARCHAR``` |
| metadata.product.name | ```'checkpoint-traffic'``` |
| metadata.product.vendor_name | ```'checkpoint'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN SEVERITY = 0 THEN 1 WHEN SEVERITY = 1 THEN 2  WHEN SEVERITY = 2 THEN 3 WHEN SEVERITY = 3 THEN 4 WHEN SEVERITY = 4 THEN 5 WHEN SEVERITY  = 'Critical'    THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN SEVERITY = 0 THEN 1 WHEN SEVERITY = 1 THEN 2  WHEN SEVERITY = 2 THEN 3 WHEN SEVERITY = 3 THEN 4 WHEN SEVERITY = 4 THEN 5 WHEN SEVERITY  = 'Critical'    THEN 5 ELSE 99 END::NUMBER``` |
| src_endpoint.hostname | ```SRC_MACHINE_NAME::VARCHAR``` |
| src_endpoint.ip | ```SRC::VARCHAR``` |
| src_endpoint.port | ```S_PORT::VARCHAR``` |
| src_endpoint.zone | ```RAW:inzone::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', time::TIMESTAMP_LTZ)``` |
| time_dt | ```time::TIMESTAMP_LTZ``` |
| traffic.bytes | ```BYTES::NUMBER``` |
| traffic.packets | ```PACKETS::NUMBER``` |
| type_name | ```CASE (400102::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```400102::NUMBER``` |
| url.path | ```RAW:http::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
