# Event Dossier: Cisco Ftd Firewall to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `cisco-firewall`
* Product name: `cisco-ftd-firewall`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.user.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', EXTRACTED_FIELDS:group::VARCHAR))``` |
| actor.user.name | ```SOURCE_USERNAME::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| dst_endpoint.ip | ```COALESCE(DESTINATION_IP, EXTRACTED_FIELDS:target_ip)::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT::VARCHAR``` |
| message | ```RAW_LOG_MESSAGE::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'cisco-ftd-firewall'``` |
| metadata.product.vendor_name | ```'cisco-firewall'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN SEVERITY = 1 THEN 6 WHEN SEVERITY = 2 THEN 5 WHEN SEVERITY = 3 THEN 4 WHEN SEVERITY = 4 THEN 3 WHEN SEVERITY = 5 THEN 2 WHEN SEVERITY = 6 THEN 1 ELSE 0 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN SEVERITY = 1 THEN 6 WHEN SEVERITY = 2 THEN 5 WHEN SEVERITY = 3 THEN 4 WHEN SEVERITY = 4 THEN 3 WHEN SEVERITY = 5 THEN 2 WHEN SEVERITY = 6 THEN 1 ELSE 0 END::NUMBER``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| src_endpoint.port | ```SOURCE_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (4001*100+99::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```4001*100+99::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
