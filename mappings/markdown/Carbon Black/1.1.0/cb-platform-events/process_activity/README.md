# Event Dossier: Cb Platform Events to OCSF class Process Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `process_activity`
* Vendor name: `cb-defense`
* Product name: `cb-platform-events`
* Event codes: `TYPE IN ('endpoint.event.procstart', 'endpoint.event.procend')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN SENSOR_ACTION = 'ACTION_ALLOW' THEN 1 WHEN SENSOR_ACTION = 'ACTION_BLOCK' THEN 2 WHEN SENSOR_ACTION is NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN SENSOR_ACTION = 'ACTION_ALLOW' THEN 1 WHEN SENSOR_ACTION = 'ACTION_BLOCK' THEN 2 WHEN SENSOR_ACTION is NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN ACTION IS NULL OR ACTION = '' THEN 0 WHEN ACTION = 'ACTION_PROCESS_TERMINATE' THEN 2 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION IS NULL OR ACTION = '' THEN 0 WHEN ACTION = 'ACTION_PROCESS_TERMINATE' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Launch' WHEN 2 THEN 'Terminate' WHEN 3 THEN 'Open' WHEN 4 THEN 'Inject' WHEN 5 THEN 'Set User ID' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'process_activity'``` |
| class_uid | ```1007``` |
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
| message | ```EVENT_DESCRIPTION::VARCHAR``` |
| metadata.event_code | ```type``` |
| metadata.product.name | ```'cb-platform-events'``` |
| metadata.product.vendor_name | ```'cb-defense'``` |
| metadata.version | ```'1.1.0'``` |
| process.cmd_line | ```PROCESS_CMDLINE::VARCHAR``` |
| process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN PROCESS_HASH_SHA256 IS NULL AND PROCESS_HASH_MD5 IS NULL THEN 0 WHEN PROCESS_HASH_SHA256 IS NOT NULL THEN 3 WHEN PROCESS_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN PROCESS_HASH_SHA256 IS NULL AND PROCESS_HASH_MD5 IS NULL THEN 0 WHEN PROCESS_HASH_SHA256 IS NOT NULL THEN 3 WHEN PROCESS_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(PROCESS_HASH_SHA256, PROCESS_HASH_MD5)::VARCHAR))``` |
| process.file.path | ```PROCESS_PATH::VARCHAR``` |
| process.parent_process.cmd_line | ```PARENT_CMDLINE::VARCHAR``` |
| process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN PARENT_HASH_SHA256 IS NULL AND PARENT_HASH_MD5 IS NULL THEN 0 WHEN PARENT_HASH_SHA256 IS NOT NULL THEN 3 WHEN PARENT_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN PARENT_HASH_SHA256 IS NULL AND PARENT_HASH_MD5 IS NULL THEN 0 WHEN PARENT_HASH_SHA256 IS NOT NULL THEN 3 WHEN PARENT_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(PARENT_HASH_SHA256, PARENT_HASH_MD5)::VARCHAR))``` |
| process.parent_process.file.path | ```PARENT_PATH::VARCHAR``` |
| process.parent_process.pid | ```PARENT_PID::NUMBER``` |
| process.parent_process.uid | ```PARENT_GUID::VARCHAR``` |
| process.pid | ```PROCESS_PID::NUMBER``` |
| process.uid | ```PROCESS_GUID::VARCHAR``` |
| process.user.name | ```PROCESS_USERNAME::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', backend_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```backend_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN ACTION IS NULL OR ACTION = '' THEN 100700 WHEN ACTION = 'ACTION_PROCESS_TERMINATE' THEN 100702 ELSE 100799 END::NUMBER) WHEN 100700 THEN 'Process Activity: Unknown' WHEN 100701 THEN 'Process Activity: Launch' WHEN 100702 THEN 'Process Activity: Terminate' WHEN 100703 THEN 'Process Activity: Open' WHEN 100704 THEN 'Process Activity: Inject' WHEN 100705 THEN 'Process Activity: Set User ID' WHEN 100799 THEN 'Process Activity: Other' END``` |
| type_uid | ```CASE WHEN ACTION IS NULL OR ACTION = '' THEN 100700 WHEN ACTION = 'ACTION_PROCESS_TERMINATE' THEN 100702 ELSE 100799 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
