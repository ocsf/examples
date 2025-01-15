# Event Dossier: Pfsense Filter Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `pfsense`
* Product name: `pfsense-filter-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN action = 'pass' THEN 1 WHEN action = 'block' THEN 2 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN action = 'pass' THEN 1 WHEN action = 'block' THEN 2 ELSE 99 END``` |
| activity_id | ```0::NUMBER``` |
| activity_name | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.pid | ```PID::NUMBER``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.direction | ```CASE (CASE WHEN DIRECTION = 'in' THEN 1 WHEN DIRECTION = 'out' THEN        2 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```CASE WHEN DIRECTION = 'in' THEN 1 WHEN DIRECTION = 'out' THEN        2 ELSE 99 END``` |
| connection_info.protocol_num | ```PROTOCOL_ID::NUMBER``` |
| connection_info.protocol_ver | ```CASE (IP_VERSION::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```IP_VERSION::NUMBER``` |
| device.interface_name | ```INTERFACE::VARCHAR``` |
| dst_endpoint.ip | ```DESTINATION_IP::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT::VARCHAR``` |
| firewall_rule.uid | ```RULE_NUMBER::VARCHAR``` |
| metadata.product.name | ```'pfsense-filter-logs'``` |
| metadata.product.vendor_name | ```'pfsense'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| src_endpoint.port | ```SOURCE_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (400100::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```400100::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
