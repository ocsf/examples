# Event Dossier: Cb Platform Events to OCSF class Win/registry Key Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_key_activity`
* Vendor name: `cb-defense`
* Product name: `cb-platform-events`
* Event codes: `TYPE = 'endpoint.event.regmod' AND ACTION ILIKE '%KEY%'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN SENSOR_ACTION = 'ACTION_ALLOW' THEN 1 WHEN SENSOR_ACTION = 'ACTION_BLOCK' THEN 2 WHEN SENSOR_ACTION is NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN SENSOR_ACTION = 'ACTION_ALLOW' THEN 1 WHEN SENSOR_ACTION = 'ACTION_BLOCK' THEN 2 WHEN SENSOR_ACTION is NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN ACTION IS NULL OR ACTION = '' THEN 0 WHEN ACTION  ILIKE '%ACTION_CREATE_KEY%' THEN 1 WHEN ACTION  ILIKE '%ACTION_DELETE_KEY%' THEN 4 WHEN ACTION  ILIKE '%ACTION_RENAME_KEY%' THEN 5 WHEN ACTION  ILIKE '%ACTION_RESTORE_KEY%' THEN 7 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION IS NULL OR ACTION = '' THEN 0 WHEN ACTION  ILIKE '%ACTION_CREATE_KEY%' THEN 1 WHEN ACTION  ILIKE '%ACTION_DELETE_KEY%' THEN 4 WHEN ACTION  ILIKE '%ACTION_RENAME_KEY%' THEN 5 WHEN ACTION  ILIKE '%ACTION_RESTORE_KEY%' THEN 7 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 2 THEN 'Read' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Security' WHEN 7 THEN 'Restore' WHEN 8 THEN 'Import' WHEN 9 THEN 'Export' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```PROCESS_CMDLINE::VARCHAR``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN PROCESS_HASH_SHA256 IS NULL AND PROCESS_HASH_MD5 IS NULL THEN 0 WHEN PROCESS_HASH_SHA256 IS NOT NULL THEN 3 WHEN PROCESS_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN PROCESS_HASH_SHA256 IS NULL AND PROCESS_HASH_MD5 IS NULL THEN 0 WHEN PROCESS_HASH_SHA256 IS NOT NULL THEN 3 WHEN PROCESS_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(PROCESS_HASH_SHA256, PROCESS_HASH_MD5)::VARCHAR))``` |
| actor.process.file.path | ```PROCESS_PATH::VARCHAR``` |
| actor.process.parent_process.cmd_line | ```PARENT_CMDLINE::VARCHAR``` |
| actor.process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN PARENT_HASH_SHA256 IS NULL AND PARENT_HASH_MD5 IS NULL THEN 0 WHEN PARENT_HASH_SHA256 IS NOT NULL THEN 3 WHEN PARENT_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN PARENT_HASH_SHA256 IS NULL AND PARENT_HASH_MD5 IS NULL THEN 0 WHEN PARENT_HASH_SHA256 IS NOT NULL THEN 3 WHEN PARENT_HASH_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(PARENT_HASH_SHA256, PARENT_HASH_MD5)::VARCHAR))``` |
| actor.process.parent_process.file.path | ```PARENT_PATH::VARCHAR``` |
| actor.process.parent_process.pid | ```PARENT_PID::NUMBER``` |
| actor.process.parent_process.uid | ```PARENT_GUID::VARCHAR``` |
| actor.process.pid | ```PROCESS_PID::NUMBER``` |
| actor.process.uid | ```PROCESS_GUID::VARCHAR``` |
| actor.process.user.name | ```PROCESS_USERNAME::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'win/registry_key_activity'``` |
| class_uid | ```201001``` |
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
| disposition | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```0::NUMBER``` |
| message | ```EVENT_DESCRIPTION::VARCHAR``` |
| metadata.event_code | ```type``` |
| metadata.product.name | ```'cb-platform-events'``` |
| metadata.product.vendor_name | ```'cb-defense'``` |
| metadata.version | ```'1.1.0'``` |
| reg_key.path | ```REGMOD_NAME::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', backend_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```backend_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN ACTION IS NULL OR ACTION = '' THEN 20100100 WHEN ACTION  ILIKE '%ACTION_CREATE_KEY%' THEN 20100101 WHEN ACTION  ILIKE '%ACTION_DELETE_KEY%' THEN 20100104 WHEN ACTION  ILIKE '%ACTION_RENAME_KEY%' THEN 20100105 WHEN ACTION  ILIKE '%ACTION_RESTORE_KEY%' THEN 20100107 ELSE 20100199 END::NUMBER) WHEN 20100100 THEN 'Registry Key Activity: Unknown' WHEN 20100101 THEN 'Registry Key Activity: Create' WHEN 20100102 THEN 'Registry Key Activity: Read' WHEN 20100103 THEN 'Registry Key Activity: Modify' WHEN 20100104 THEN 'Registry Key Activity: Delete' WHEN 20100105 THEN 'Registry Key Activity: Rename' WHEN 20100106 THEN 'Registry Key Activity: Set Security' WHEN 20100107 THEN 'Registry Key Activity: Restore' WHEN 20100108 THEN 'Registry Key Activity: Import' WHEN 20100109 THEN 'Registry Key Activity: Export' WHEN 20100199 THEN 'Registry Key Activity: Other' END``` |
| type_uid | ```CASE WHEN ACTION IS NULL OR ACTION = '' THEN 20100100 WHEN ACTION  ILIKE '%ACTION_CREATE_KEY%' THEN 20100101 WHEN ACTION  ILIKE '%ACTION_DELETE_KEY%' THEN 20100104 WHEN ACTION  ILIKE '%ACTION_RENAME_KEY%' THEN 20100105 WHEN ACTION  ILIKE '%ACTION_RESTORE_KEY%' THEN 20100107 ELSE 20100199 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤