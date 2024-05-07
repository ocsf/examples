# Event Dossier: Cisco Asa Firewall to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `cisco-firewall`
* Product name: `cisco-asa-firewall`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```6::NUMBER``` |
| activity_name | ```CASE (6::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.user.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', EXTRACTED_FIELDS:group::VARCHAR))``` |
| actor.user.name | ```SOURCE_USERNAME::VARCHAR``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```LOWER(EXTRACTED_FIELDS:protocol)::VARCHAR``` |
| device.ip | ```FIREWALL_IP::VARCHAR``` |
| dst_endpoint.ip | ```DESTINATION_IP::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT::VARCHAR``` |
| firewall_rule.uid | ```FIREWALL_IDENTIFIER::VARCHAR``` |
| message | ```RAW_LOG_MESSAGE::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'cisco-asa-firewall'``` |
| metadata.product.vendor_name | ```'cisco-firewall'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (SEVERITY::VARCHAR) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```SEVERITY::VARCHAR``` |
| src_endpoint.hostname | ```COALESCE(EXTRACTED_FIELDS:initiator_hostname,EXTRACTED_FIELDS:original_initiator_hostname)::VARCHAR``` |
| src_endpoint.ip | ```COALESCE(SOURCE_IP, EXTRACTED_FIELDS:original_initiator_ip, EXTRACTED_FIELDS:initiator_ip)::VARCHAR``` |
| src_endpoint.port | ```COALESCE(SOURCE_PORT, EXTRACTED_FIELDS:initiator_port)::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| traffic.bytes_in | ```EXTRACTED_FIELDS:responder_bytes::NUMBER``` |
| traffic.bytes_out | ```EXTRACTED_FIELDS:initiator_bytes::NUMBER``` |
| type_name | ```CASE (400106::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```400106::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
