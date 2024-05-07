# Event Dossier: Cb Platform Events to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `cb-defense`
* Product name: `cb-platform-events`
* Event codes: `TYPE IN ('endpoint.event.netconn', 'endpoint.event.netconn_proxy')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN SENSOR_ACTION = 'ACTION_ALLOW' THEN 1 WHEN SENSOR_ACTION = 'ACTION_BLOCK' THEN 2 WHEN SENSOR_ACTION is NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN SENSOR_ACTION = 'ACTION_ALLOW' THEN 1 WHEN SENSOR_ACTION = 'ACTION_BLOCK' THEN 2 WHEN SENSOR_ACTION is NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```PROCESS_CMDLINE::VARCHAR``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN PROCESS_HASH_SHA256 IS NULL AND PROCESS_HASH_MD5 IS NULL THEN 0 WHEN PROCESS_HASH_SHA256 IS NOT NULL THEN 3 WHEN PROCESS_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN PROCESS_HASH_SHA256 IS NULL AND PROCESS_HASH_MD5 IS NULL THEN 0 WHEN PROCESS_HASH_SHA256 IS NOT NULL THEN 3 WHEN PROCESS_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER::NUMBER, 'value', COALESCE(PROCESS_HASH_SHA256, PROCESS_HASH_MD5)::VARCHAR))``` |
| actor.process.file.path | ```PROCESS_PATH::VARCHAR``` |
| actor.process.parent_process.cmd_line | ```PARENT_CMDLINE::VARCHAR``` |
| actor.process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN PARENT_HASH_SHA256 IS NULL AND PARENT_HASH_MD5 IS NULL THEN 0 WHEN PARENT_HASH_SHA256 IS NOT NULL THEN 3 WHEN PARENT_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN PARENT_HASH_SHA256 IS NULL AND PARENT_HASH_MD5 IS NULL THEN 0 WHEN PARENT_HASH_SHA256 IS NOT NULL THEN 3 WHEN PARENT_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(PARENT_HASH_SHA256, PARENT_HASH_MD5)::VARCHAR))``` |
| actor.process.parent_process.file.path | ```PARENT_PATH::VARCHAR``` |
| actor.process.parent_process.pid | ```PARENT_PID::NUMBER``` |
| actor.process.parent_process.uid | ```PARENT_GUID::VARCHAR``` |
| actor.process.pid | ```PROCESS_PID::NUMBER``` |
| actor.process.uid | ```PROCESS_GUID::VARCHAR``` |
| actor.process.user.name | ```PROCESS_USERNAME::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.direction | ```CASE (IFF(NETCONN_INBOUND = 'True', 1 , 0)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```IFF(NETCONN_INBOUND = 'True', 1 , 0)::NUMBER``` |
| connection_info.protocol_name | ```CASE WHEN NETCONN_PROTOCOL = 'PROTO_ICMP' THEN 'icmp' WHEN NETCONN_PROTOCOL = 'PROTO_TCP' THEN 'tcp' WHEN NETCONN_PROTOCOL = 'PROTO_UDP' THEN 'udp' ELSE NULL END::VARCHAR``` |
| connection_info.protocol_num | ```CASE WHEN NETCONN_PROTOCOL = 'PROTO_ICMP' THEN 1 WHEN NETCONN_PROTOCOL = 'PROTO_TCP' THEN 6 WHEN NETCONN_PROTOCOL = 'PROTO_UDP' THEN 17 ELSE NULL END::NUMBER``` |
| device.first_seen_time | ```date_part('epoch_milliseconds', DEVICE_TIMESTAMP::TIMESTAMP_LTZ)``` |
| device.first_seen_time_dt | ```DEVICE_TIMESTAMP::TIMESTAMP_LTZ``` |
| device.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', DEVICE_GROUP::VARCHAR))``` |
| device.ip | ```DEVICE_EXTERNAL_IP::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.org.uid | ```ORG_KEY::VARCHAR``` |
| device.os.name | ```DEVICE_OS::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN DEVICE_OS ='WINDOWS' THEN 100 WHEN DEVICE_OS = 'LINUX' THEN 200 WHEN DEVICE_OS = 'MAC' THEN 300 WHEN DEVICE_OS is NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN DEVICE_OS ='WINDOWS' THEN 100 WHEN DEVICE_OS = 'LINUX' THEN 200 WHEN DEVICE_OS = 'MAC' THEN 300 WHEN DEVICE_OS is NULL THEN 0 ELSE 99 END::NUMBER``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| dst_endpoint.domain | ```NETCONN_DOMAIN::VARCHAR``` |
| dst_endpoint.ip | ```REMOTE_IP::VARCHAR``` |
| dst_endpoint.port | ```REMOTE_PORT::VARCHAR``` |
| message | ```EVENT_DESCRIPTION::VARCHAR``` |
| metadata.event_code | ```type``` |
| metadata.product.name | ```'cb-platform-events'``` |
| metadata.product.vendor_name | ```'cb-defense'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```LOCAL_IP::VARCHAR``` |
| src_endpoint.port | ```LOCAL_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', backend_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```backend_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (400101::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```400101::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
