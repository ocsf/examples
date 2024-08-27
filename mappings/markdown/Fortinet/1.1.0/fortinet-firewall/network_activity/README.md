# Event Dossier: Fortinet Firewall to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `fortinet`
* Product name: `fortinet-firewall`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION='start' THEN 1 WHEN ACTION='accept' THEN 1 WHEN ACTION='permit' THEN 1 WHEN ACTION='close' THEN 2 WHEN ACTION='Reject' THEN 2 WHEN ACTION='block' THEN 2 WHEN ACTION='deny' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION='start' THEN 1 WHEN ACTION='accept' THEN 1 WHEN ACTION='permit' THEN 1 WHEN ACTION='close' THEN 2 WHEN ACTION='Reject' THEN 2 WHEN ACTION='block' THEN 2 WHEN ACTION='deny' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN TYPE is null then 0 WHEN TYPE = 'traffic' then 6 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN TYPE is null then 0 WHEN TYPE = 'traffic' then 6 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| authorizations.policy.uid | ```POLICY_ID::VARCHAR``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```SERVICE::VARCHAR``` |
| connection_info.protocol_num | ```PROTO::NUMBER``` |
| connection_info.session.count | ```TOTAL_SESSION::NUMBER``` |
| connection_info.session.uid | ```SESSION_ID::VARCHAR``` |
| device.name | ```DEV_NAME::VARCHAR``` |
| device.type | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```0::NUMBER``` |
| device.uid | ```DEV_ID::VARCHAR``` |
| dst_endpoint.interface_name | ```DST_INTF::VARCHAR``` |
| dst_endpoint.ip | ```DST_IP::VARCHAR``` |
| dst_endpoint.location.country | ```DST_COUNTRY::VARCHAR``` |
| dst_endpoint.port | ```DST_PORT::NUMBER``` |
| duration | ```DURATION::NUMBER``` |
| message | ```MSG::VARCHAR``` |
| metadata.event_code | ```type``` |
| metadata.product.name | ```'fortinet-firewall'``` |
| metadata.product.vendor_name | ```'fortinet'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN LEVEL='information' THEN 1 WHEN LEVEL='info' THEN 1 WHEN LEVEL='notice' THEN 2 WHEN LEVEL='warning' THEN 3 WHEN LEVEL='alert' THEN 4 WHEN LEVEL='critical' THEN 5 WHEN LEVEL='error' THEN 6 WHEN LEVEL IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN LEVEL='information' THEN 1 WHEN LEVEL='info' THEN 1 WHEN LEVEL='notice' THEN 2 WHEN LEVEL='warning' THEN 3 WHEN LEVEL='alert' THEN 4 WHEN LEVEL='critical' THEN 5 WHEN LEVEL='error' THEN 6 WHEN LEVEL IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| src_endpoint.interface_name | ```SRC_INTF::VARCHAR``` |
| src_endpoint.ip | ```SRC_IP::VARCHAR``` |
| src_endpoint.location.country | ```SRC_COUNTRY::VARCHAR``` |
| src_endpoint.port | ```SRC_PORT::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| traffic.bytes_in | ```RCVD_BYTE::NUMBER``` |
| traffic.bytes_out | ```SENT_BYTE::NUMBER``` |
| traffic.packets_in | ```RCVD_PKT::NUMBER``` |
| traffic.packets_out | ```SENT_PKT::NUMBER``` |
| type_name | ```CASE ((400100 + (CASE WHEN TYPE is null then 0 WHEN TYPE = 'traffic' then 6 ELSE 99 END))::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```(400100 + (CASE WHEN TYPE is null then 0 WHEN TYPE = 'traffic' then 6 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
