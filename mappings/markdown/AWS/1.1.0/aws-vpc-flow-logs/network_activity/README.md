# Event Dossier: Aws Vpc Flow Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `aws`
* Product name: `aws-vpc-flow-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION = 'Block' then 2 WHEN ACTION = 'ACCEPT' then 1 WHEN ACTION is null then 0 ELSE 99 END::int::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION = 'Block' then 2 WHEN ACTION = 'ACCEPT' then 1 WHEN ACTION is null then 0 ELSE 99 END::int::NUMBER``` |
| activity_id | ```0::NUMBER``` |
| activity_name | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.user.account.uid | ```ACCOUNT_ID::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| cloud.region | ```REGION::VARCHAR``` |
| connection_info.direction | ```CASE (CASE FLOW_DIRECTION WHEN 'ingress' THEN 1::NUMBER WHEN 'egress' THEN 2::NUMBER ELSE 0::NUMBER END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```CASE FLOW_DIRECTION WHEN 'ingress' THEN 1::NUMBER WHEN 'egress' THEN 2::NUMBER ELSE 0::NUMBER END``` |
| connection_info.protocol_num | ```IANA_PROTOCOL_NUMBER::NUMBER``` |
| connection_info.protocol_ver | ```CASE (CASE TRAFFIC_TYPE WHEN 'IPv4' THEN 4::NUMBER WHEN 'IPv6' THEN 6 ELSE 0 END) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```CASE TRAFFIC_TYPE WHEN 'IPv4' THEN 4::NUMBER WHEN 'IPv6' THEN 6 ELSE 0 END``` |
| connection_info.tcp_flags | ```TCP_FLAGS::NUMBER``` |
| device.instance_uid | ```INSTANCE_ID::VARCHAR``` |
| device.interface_uid | ```INTERFACE_ID::VARCHAR``` |
| device.subnet_uid | ```SUBNET_ID::VARCHAR``` |
| device.vpc_uid | ```VPC_ID::VARCHAR``` |
| dst_endpoint.ip | ```DESTINATION_ADDRESS::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', END_TIME::TIMESTAMP_LTZ)``` |
| end_time_dt | ```END_TIME::TIMESTAMP_LTZ``` |
| metadata.product.name | ```'aws-vpc-flow-logs'``` |
| metadata.product.vendor_name | ```'aws'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```1::NUMBER``` |
| src_endpoint.ip | ```SOURCE_ADDRESS::VARCHAR``` |
| src_endpoint.port | ```SOURCE_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', start_time::TIMESTAMP_LTZ)``` |
| time_dt | ```start_time::TIMESTAMP_LTZ``` |
| traffic.bytes_out | ```TOTAL_BYTES_TRANSFERRED::NUMBER``` |
| traffic.packets_out | ```TOTAL_PACKETS_TRANSFERRED::NUMBER``` |
| type_name | ```CASE (400100::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```400100::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
