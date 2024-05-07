# Event Dossier: Mdatp Device Process Events to OCSF class Process Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `process_activity`
* Vendor name: `mdatp`
* Product name: `mdatp-device-process-events`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE='ProcessCreated' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE='ProcessCreated' THEN 1 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE='ProcessCreated' THEN 1 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE='ProcessCreated' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Launch' WHEN 2 THEN 'Terminate' WHEN 3 THEN 'Open' WHEN 4 THEN 'Inject' WHEN 5 THEN 'Set User ID' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'process_activity'``` |
| class_uid | ```1007``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| metadata.product.name | ```'mdatp-device-process-events'``` |
| metadata.product.vendor_name | ```'mdatp'``` |
| metadata.version | ```'1.1.0'``` |
| process.cmd_line | ```PROCESS_COMMAND_LINE::VARCHAR``` |
| process.created_time | ```date_part('epoch_milliseconds', PROCESS_CREATION_TIME::TIMESTAMP_LTZ)``` |
| process.created_time_dt | ```PROCESS_CREATION_TIME::TIMESTAMP_LTZ``` |
| process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN SHA256 IS NULL AND SHA1 IS NULL AND MD5 IS NULL THEN 0 WHEN SHA256 IS NOT NULL THEN 3 WHEN SHA1 IS NOT NULL THEN 2 WHEN MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN SHA256 IS NULL AND SHA1 IS NULL AND MD5 IS NULL THEN 0 WHEN SHA256 IS NOT NULL THEN 3 WHEN SHA1 IS NOT NULL THEN 2 WHEN MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(SHA256, SHA1, MD5)::VARCHAR))``` |
| process.file.name | ```FILE_NAME::VARCHAR``` |
| process.file.path | ```FOLDER_PATH::VARCHAR``` |
| process.integrity | ```CASE (CASE WHEN PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN PROCESS_INTEGRITY_LEVEL = 'Untrusted' THEN 1 WHEN PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Untrusted' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'System' WHEN 6 THEN 'Protected' WHEN 99 THEN 'Other' END``` |
| process.integrity_id | ```CASE WHEN PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN PROCESS_INTEGRITY_LEVEL = 'Untrusted' THEN 1 WHEN PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER``` |
| process.parent_process.cmd_line | ```INITIATING_PROCESS_COMMAND_LINE::VARCHAR``` |
| process.parent_process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ)``` |
| process.parent_process.created_time_dt | ```INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ``` |
| process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN INITIATING_PROCESS_SHA256 IS NULL AND INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA256 IS NOT NULL THEN 3 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN INITIATING_PROCESS_SHA256 IS NULL AND INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA256 IS NOT NULL THEN 3 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(INITIATING_PROCESS_SHA256, INITIATING_PROCESS_SHA1, INITIATING_PROCESS_MD5)::VARCHAR))``` |
| process.parent_process.file.name | ```INITIATING_PROCESS_FILE_NAME::VARCHAR``` |
| process.parent_process.file.path | ```INITIATING_PROCESS_FOLDER_PATH::VARCHAR``` |
| process.parent_process.integrity | ```CASE (CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Untrusted' THEN 1 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Untrusted' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'System' WHEN 6 THEN 'Protected' WHEN 99 THEN 'Other' END``` |
| process.parent_process.integrity_id | ```CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Untrusted' THEN 1 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER``` |
| process.parent_process.parent_process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ)``` |
| process.parent_process.parent_process.created_time_dt | ```INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ``` |
| process.parent_process.parent_process.file.name | ```INITIATING_PROCESS_PARENT_FILE_NAME::VARCHAR``` |
| process.parent_process.parent_process.pid | ```INITIATING_PROCESS_PARENT_ID::NUMBER``` |
| process.parent_process.pid | ```INITIATING_PROCESS_ID::NUMBER``` |
| process.parent_process.user.domain | ```INITIATING_PROCESS_ACCOUNT_DOMAIN::VARCHAR``` |
| process.parent_process.user.name | ```INITIATING_PROCESS_ACCOUNT_NAME::VARCHAR``` |
| process.parent_process.user.uid | ```INITIATING_PROCESS_ACCOUNT_SID::VARCHAR``` |
| process.pid | ```PROCESS_ID::NUMBER``` |
| process.user.domain | ```ACCOUNT_DOMAIN::VARCHAR``` |
| process.user.name | ```ACCOUNT_NAME::VARCHAR``` |
| process.user.uid | ```ACCOUNT_SID::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((100700 + (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE='ProcessCreated' THEN 1 ELSE 99 END))::NUMBER) WHEN 100700 THEN 'Process Activity: Unknown' WHEN 100701 THEN 'Process Activity: Launch' WHEN 100702 THEN 'Process Activity: Terminate' WHEN 100703 THEN 'Process Activity: Open' WHEN 100704 THEN 'Process Activity: Inject' WHEN 100705 THEN 'Process Activity: Set User ID' WHEN 100799 THEN 'Process Activity: Other' END``` |
| type_uid | ```(100700 + (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE='ProcessCreated' THEN 1 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
