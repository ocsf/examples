# Event Dossier: Sentinelone Raw Events V2 to OCSF class File Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `file_activity`
* Vendor name: `sentinelone`
* Product name: `sentinelone-raw-events-v2`
* Event codes: `EVENT_TYPE IN ('File Creation', 'File Deletion', 'File Modification', 'File Rename')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'File Creation' THEN 1 WHEN EVENT_TYPE = 'File Modification' THEN 3 WHEN EVENT_TYPE = 'File Deletion' THEN 4 WHEN EVENT_TYPE = 'File Rename' THEN 5 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'File Creation' THEN 1 WHEN EVENT_TYPE = 'File Modification' THEN 3 WHEN EVENT_TYPE = 'File Deletion' THEN 4 WHEN EVENT_TYPE = 'File Rename' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 10 THEN 'Encrypt' WHEN 11 THEN 'Decrypt' WHEN 12 THEN 'Mount' WHEN 13 THEN 'Unmount' WHEN 14 THEN 'Open' WHEN 2 THEN 'Read' WHEN 3 THEN 'Update' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Attributes' WHEN 7 THEN 'Set Security' WHEN 8 THEN 'Get Attributes' WHEN 9 THEN 'Get Security' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```SRC_PROCESS_CMDLINE::VARCHAR``` |
| actor.process.container.image.path | ```SRC_PROCESS_IMAGE_PATH::VARCHAR``` |
| actor.process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_START_TIME::TIMESTAMP_LTZ)``` |
| actor.process.created_time_dt | ```SRC_PROCESS_START_TIME::TIMESTAMP_LTZ``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(SRC_PROCESS_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(SRC_PROCESS_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER))``` |
| actor.process.name | ```SRC_PROCESS_NAME::VARCHAR``` |
| actor.process.parent_process.cmd_line | ```SRC_PROCESS_PARENT_CMDLINE::VARCHAR``` |
| actor.process.parent_process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.created_time_dt | ```SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(SRC_PROCESS_PARENT_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(SRC_PROCESS_PARENT_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER, 'value', SRC_PROCESS_PARENT_IMAGE_SHA256::VARCHAR))``` |
| actor.process.parent_process.name | ```SRC_PROCESS_PARENT_NAME::VARCHAR``` |
| actor.process.parent_process.pid | ```SRC_PROCESS_PARENT_PID::NUMBER``` |
| actor.process.parent_process.uid | ```SRC_PROCESS_PARENT_UID::VARCHAR``` |
| actor.process.pid | ```SRC_PROCESS_PID::NUMBER``` |
| actor.process.uid | ```SRC_PROCESS_UID::VARCHAR``` |
| actor.process.user.name | ```SRC_PROCESS_USER_NAME::VARCHAR``` |
| actor.session.uid | ```LOGIN_USER_SID::VARCHAR``` |
| actor.user.name | ```LOGIN_USER_NAME::VARCHAR``` |
| class_name | ```'file_activity'``` |
| class_uid | ```1001``` |
| device.hostname | ```COMPUTER_NAME::VARCHAR``` |
| device.ip | ```SRC_IP_ADDRESS::VARCHAR``` |
| device.os.name | ```OS_NAME::VARCHAR``` |
| device.os.type | ```CASE (CASE OS_FAMILY WHEN 'linux' THEN 200 WHEN 'windows' THEN 100 WHEN 'osx' THEN 300 WHEN null THEN 0 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE OS_FAMILY WHEN 'linux' THEN 200 WHEN 'windows' THEN 100 WHEN 'osx' THEN 300 WHEN null THEN 0 ELSE 99 END``` |
| file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(TGT_FILE_SHA256 IS NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(TGT_FILE_SHA256 IS NULL, 0, 3)::NUMBER, 'value', TGT_FILE_SHA256::VARCHAR))``` |
| file.path | ```TGT_FILE_PATH::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'sentinelone-raw-events-v2'``` |
| metadata.product.vendor_name | ```'sentinelone'``` |
| metadata.version | ```'1.1.0'``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((100100 + (CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'File Creation' THEN 1 WHEN EVENT_TYPE = 'File Modification' THEN 3 WHEN EVENT_TYPE = 'File Deletion' THEN 4 WHEN EVENT_TYPE = 'File Rename' THEN 5 ELSE 99 END))::NUMBER) WHEN 100100 THEN 'File System Activity: Unknown' WHEN 100101 THEN 'File System Activity: Create' WHEN 100102 THEN 'File System Activity: Read' WHEN 100103 THEN 'File System Activity: Update' WHEN 100104 THEN 'File System Activity: Delete' WHEN 100105 THEN 'File System Activity: Rename' WHEN 100106 THEN 'File System Activity: Set Attributes' WHEN 100107 THEN 'File System Activity: Set Security' WHEN 100108 THEN 'File System Activity: Get Attributes' WHEN 100109 THEN 'File System Activity: Get Security' WHEN 100110 THEN 'File System Activity: Encrypt' WHEN 100111 THEN 'File System Activity: Decrypt' WHEN 100112 THEN 'File System Activity: Mount' WHEN 100113 THEN 'File System Activity: Unmount' WHEN 100114 THEN 'File System Activity: Open' WHEN 100199 THEN 'File System Activity: Other' END``` |
| type_uid | ```(100100 + (CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'File Creation' THEN 1 WHEN EVENT_TYPE = 'File Modification' THEN 3 WHEN EVENT_TYPE = 'File Deletion' THEN 4 WHEN EVENT_TYPE = 'File Rename' THEN 5 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
