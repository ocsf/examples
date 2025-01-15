# Event Dossier: Sentinelone Raw Events V2 to OCSF class Process Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `process_activity`
* Vendor name: `sentinelone`
* Product name: `sentinelone-raw-events-v2`
* Event codes: `event_type = 'Process Creation'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```1::NUMBER``` |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Launch' WHEN 2 THEN 'Terminate' WHEN 3 THEN 'Open' WHEN 4 THEN 'Inject' WHEN 5 THEN 'Set User ID' WHEN 99 THEN 'Other' END``` |
| actor.session.uid | ```LOGIN_USER_SID::VARCHAR``` |
| actor.user.name | ```LOGIN_USER_NAME::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'process_activity'``` |
| class_uid | ```1007``` |
| device.name | ```COMPUTER_NAME::VARCHAR``` |
| device.os.name | ```OS_NAME::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN OS_FAMILY = 'windows' THEN 100 WHEN OS_FAMILY = 'linux' THEN 200 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS_FAMILY = 'windows' THEN 100 WHEN OS_FAMILY = 'linux' THEN 200 ELSE 99 END::NUMBER``` |
| device.uid | ```AGENT_UUID::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'sentinelone-raw-events-v2'``` |
| metadata.product.vendor_name | ```'sentinelone'``` |
| metadata.version | ```'1.1.0'``` |
| process.cmd_line | ```SRC_PROCESS_CMDLINE::VARCHAR``` |
| process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_START_TIME::TIMESTAMP_LTZ)``` |
| process.created_time_dt | ```SRC_PROCESS_START_TIME::TIMESTAMP_LTZ``` |
| process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (iff(SRC_PROCESS_IMAGE_SHA256 is NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', iff(SRC_PROCESS_IMAGE_SHA256 is NULL, 0, 3)::NUMBER, 'value', iff(SRC_PROCESS_IMAGE_SHA256 is NULL, NULL, SRC_PROCESS_IMAGE_SHA256)::VARCHAR))``` |
| process.file.path | ```SRC_PROCESS_IMAGE_PATH::VARCHAR``` |
| process.name | ```SRC_PROCESS_NAME::VARCHAR``` |
| process.parent_process.cmd_line | ```SRC_PROCESS_PARENT_CMDLINE::VARCHAR``` |
| process.parent_process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ)``` |
| process.parent_process.created_time_dt | ```SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ``` |
| process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (iff(SRC_PROCESS_PARENT_IMAGE_SHA256 is NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', iff(SRC_PROCESS_PARENT_IMAGE_SHA256 is NULL, 0, 3)::NUMBER, 'value', iff(SRC_PROCESS_PARENT_IMAGE_SHA256 is NULL, NULL, SRC_PROCESS_PARENT_IMAGE_SHA256)::VARCHAR))``` |
| process.parent_process.name | ```SRC_PROCESS_PARENT_NAME::VARCHAR``` |
| process.parent_process.pid | ```SRC_PROCESS_PARENT_PID::NUMBER``` |
| process.parent_process.uid | ```SRC_PROCESS_PARENT_UID::VARCHAR``` |
| process.pid | ```SRC_PROCESS_PID::NUMBER``` |
| process.uid | ```SRC_PROCESS_UID::VARCHAR``` |
| process.user.name | ```SRC_PROCESS_USER_NAME::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (100799::NUMBER) WHEN 100700 THEN 'Process Activity: Unknown' WHEN 100701 THEN 'Process Activity: Launch' WHEN 100702 THEN 'Process Activity: Terminate' WHEN 100703 THEN 'Process Activity: Open' WHEN 100704 THEN 'Process Activity: Inject' WHEN 100705 THEN 'Process Activity: Set User ID' WHEN 100799 THEN 'Process Activity: Other' END``` |
| type_uid | ```100799::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
