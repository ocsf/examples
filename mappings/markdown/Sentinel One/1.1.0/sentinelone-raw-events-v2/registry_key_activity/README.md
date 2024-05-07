# Event Dossier: Sentinelone Raw Events V2 to OCSF class Win/registry Key Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_key_activity`
* Vendor name: `sentinelone`
* Product name: `sentinelone-raw-events-v2`
* Event codes: `EVENT_TYPE ILIKE '%Registry Key%'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'Registry Key Create' THEN 1 WHEN EVENT_TYPE = 'Registry Key Security Changed' THEN 3 WHEN EVENT_TYPE = 'Registry Key Delete' THEN 4 WHEN EVENT_TYPE = 'Registry Key Rename' THEN 5 WHEN EVENT_TYPE = 'Registry Key Export' THEN 9 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'Registry Key Create' THEN 1 WHEN EVENT_TYPE = 'Registry Key Security Changed' THEN 3 WHEN EVENT_TYPE = 'Registry Key Delete' THEN 4 WHEN EVENT_TYPE = 'Registry Key Rename' THEN 5 WHEN EVENT_TYPE = 'Registry Key Export' THEN 9 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 2 THEN 'Read' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Security' WHEN 7 THEN 'Restore' WHEN 8 THEN 'Import' WHEN 9 THEN 'Export' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```SRC_PROCESS_CMDLINE::VARCHAR``` |
| actor.process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_START_TIME::TIMESTAMP_LTZ)``` |
| actor.process.created_time_dt | ```SRC_PROCESS_START_TIME::TIMESTAMP_LTZ``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (iff(SRC_PROCESS_IMAGE_SHA256 is NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', iff(SRC_PROCESS_IMAGE_SHA256 is NULL, 0, 3)::NUMBER, 'value', iff(SRC_PROCESS_IMAGE_SHA256 is NULL, NULL, SRC_PROCESS_IMAGE_SHA256)::VARCHAR))``` |
| actor.process.file.path | ```SRC_PROCESS_IMAGE_PATH::VARCHAR``` |
| actor.process.name | ```SRC_PROCESS_NAME::VARCHAR``` |
| actor.process.parent_process.cmd_line | ```SRC_PROCESS_PARENT_CMDLINE::VARCHAR``` |
| actor.process.parent_process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.created_time_dt | ```SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (iff(SRC_PROCESS_PARENT_IMAGE_SHA256 is NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', iff(SRC_PROCESS_PARENT_IMAGE_SHA256 is NULL, 0, 3)::NUMBER, 'value', iff(SRC_PROCESS_PARENT_IMAGE_SHA256 is NULL, NULL, SRC_PROCESS_PARENT_IMAGE_SHA256)::VARCHAR))``` |
| actor.process.parent_process.name | ```SRC_PROCESS_PARENT_NAME::VARCHAR``` |
| actor.process.parent_process.pid | ```SRC_PROCESS_PARENT_PID::NUMBER``` |
| actor.process.parent_process.uid | ```SRC_PROCESS_PARENT_UID::VARCHAR``` |
| actor.process.pid | ```SRC_PROCESS_PID::NUMBER``` |
| actor.process.uid | ```SRC_PROCESS_UID::VARCHAR``` |
| actor.process.user.name | ```SRC_PROCESS_USER_NAME::VARCHAR``` |
| actor.session.uid | ```LOGIN_USER_SID::VARCHAR``` |
| actor.user.name | ```LOGIN_USER_NAME::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'win/registry_key_activity'``` |
| class_uid | ```201001``` |
| device.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('uid', GET(RAW, 'group.id')::VARCHAR))``` |
| device.name | ```COMPUTER_NAME::VARCHAR``` |
| device.os.name | ```OS_NAME::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN OS_FAMILY IS NULL THEN 0 WHEN OS_FAMILY = 'windows' THEN 100 WHEN OS_FAMILY = 'linux' THEN 200 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS_FAMILY IS NULL THEN 0 WHEN OS_FAMILY = 'windows' THEN 100 WHEN OS_FAMILY = 'linux' THEN 200 ELSE 99 END::NUMBER``` |
| device.uid | ```AGENT_UUID::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'sentinelone-raw-events-v2'``` |
| metadata.product.vendor_name | ```'sentinelone'``` |
| metadata.version | ```'1.1.0'``` |
| reg_key.path | ```GET(RAW, 'registry.keyPath')::VARCHAR``` |
| severity | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```99::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN EVENT_TYPE IS NULL THEN 20100100 WHEN EVENT_TYPE = 'Registry Key Create' THEN 20100101 WHEN EVENT_TYPE = 'Registry Key Security Changed' THEN 20100103 WHEN EVENT_TYPE = 'Registry Key Delete' THEN 20100104 WHEN EVENT_TYPE = 'Registry Key Rename' THEN 20100105 WHEN EVENT_TYPE = 'Registry Key Export' THEN 20100109 ELSE 20100199 END::NUMBER) WHEN 20100100 THEN 'Registry Key Activity: Unknown' WHEN 20100101 THEN 'Registry Key Activity: Create' WHEN 20100102 THEN 'Registry Key Activity: Read' WHEN 20100103 THEN 'Registry Key Activity: Modify' WHEN 20100104 THEN 'Registry Key Activity: Delete' WHEN 20100105 THEN 'Registry Key Activity: Rename' WHEN 20100106 THEN 'Registry Key Activity: Set Security' WHEN 20100107 THEN 'Registry Key Activity: Restore' WHEN 20100108 THEN 'Registry Key Activity: Import' WHEN 20100109 THEN 'Registry Key Activity: Export' WHEN 20100199 THEN 'Registry Key Activity: Other' END``` |
| type_uid | ```CASE WHEN EVENT_TYPE IS NULL THEN 20100100 WHEN EVENT_TYPE = 'Registry Key Create' THEN 20100101 WHEN EVENT_TYPE = 'Registry Key Security Changed' THEN 20100103 WHEN EVENT_TYPE = 'Registry Key Delete' THEN 20100104 WHEN EVENT_TYPE = 'Registry Key Rename' THEN 20100105 WHEN EVENT_TYPE = 'Registry Key Export' THEN 20100109 ELSE 20100199 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
