# Event Dossier: Silverpeak Firewall Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `silverpeak`
* Product name: `silverpeak-firewall-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'drop' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'drop' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN REASON = 'flow create' THEN 1 WHEN REASON = 'flow end' THEN 2 WHEN REASON = 'security policy deny' THEN 5 WHEN REASON IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN REASON = 'flow create' THEN 1 WHEN REASON = 'flow end' THEN 2 WHEN REASON = 'security policy deny' THEN 5 WHEN REASON IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| app_name | ```APPLICATION::VARCHAR``` |
| authorizations.policy.name | ```POLICY::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.direction | ```CASE (CASE WHEN DIRECTION = 'Inbound' THEN 1 WHEN DIRECTION = 'Outbound' THEN 2 WHEN DIRECTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```CASE WHEN DIRECTION = 'Inbound' THEN 1 WHEN DIRECTION = 'Outbound' THEN 2 WHEN DIRECTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| connection_info.protocol_name | ```PROTOCOL::VARCHAR``` |
| connection_info.protocol_num | ```CASE WHEN PROTOCOL = 'icmp' THEN 1 WHEN PROTOCOL = 'tcp' THEN 6 WHEN PROTOCOL = 'udp' THEN 17 WHEN PROTOCOL IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(SOURCE_ADDRESS, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(SOURCE_ADDRESS, 'INET'):family::NUMBER``` |
| connection_info.tcp_flags | ```TRY_CAST(TCP_FLAGS AS NUMBER)::NUMBER``` |
| connection_info.uid | ```FLOW_ID::VARCHAR``` |
| disposition | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```0::NUMBER``` |
| dst_endpoint.hostname | ```HOST::VARCHAR``` |
| dst_endpoint.interface_name | ```INTERFACE_IMPACTED::VARCHAR``` |
| dst_endpoint.ip | ```DESTINATION_ADDRESS::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT ::VARCHAR``` |
| dst_endpoint.zone | ```TO_ZONE::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', END_TIME::VARCHAR::TIMESTAMP_LTZ)``` |
| end_time_dt | ```END_TIME::VARCHAR::TIMESTAMP_LTZ``` |
| metadata.event_code | ```log_level``` |
| metadata.product.name | ```'silverpeak-firewall-logs'``` |
| metadata.product.vendor_name | ```'silverpeak'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.interface_name | ```INTERFACE_ORIGIN::VARCHAR``` |
| src_endpoint.ip | ```SOURCE_ADDRESS::VARCHAR``` |
| src_endpoint.port | ```SOURCE_PORT ::VARCHAR``` |
| src_endpoint.proxy_endpoint.ip | ```NAT_IP_ADDRESS_ORIGIN::VARCHAR``` |
| src_endpoint.proxy_endpoint.port | ```NAT_TCP_UDP_PORT_ORIGIN::VARCHAR``` |
| src_endpoint.svc_name | ```IP_SERVICE_TYPE::VARCHAR``` |
| src_endpoint.zone | ```FROM_ZONE::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', START_TIME::VARCHAR::TIMESTAMP_LTZ)``` |
| start_time_dt | ```START_TIME::VARCHAR::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'drop' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'drop' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| traffic.bytes | ```RECEIVED_OCTETS + TRANSMITTED_OCTETS::NUMBER``` |
| traffic.bytes_in | ```RECEIVED_OCTETS::NUMBER``` |
| traffic.bytes_out | ```TRANSMITTED_OCTETS::NUMBER``` |
| traffic.packets | ```RECEIVED_PACKETS + TRANSMITTED_PACKETS::NUMBER``` |
| traffic.packets_in | ```RECEIVED_PACKETS::NUMBER``` |
| traffic.packets_out | ```TRANSMITTED_PACKETS::NUMBER``` |
| type_name | ```CASE (CASE WHEN REASON = 'flow create' THEN 400101 WHEN REASON = 'flow end' THEN 400102 WHEN REASON = 'security policy deny' THEN 400105 WHEN REASON IS NULL THEN 400100 ELSE 400199 END::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```CASE WHEN REASON = 'flow create' THEN 400101 WHEN REASON = 'flow end' THEN 400102 WHEN REASON = 'security policy deny' THEN 400105 WHEN REASON IS NULL THEN 400100 ELSE 400199 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
