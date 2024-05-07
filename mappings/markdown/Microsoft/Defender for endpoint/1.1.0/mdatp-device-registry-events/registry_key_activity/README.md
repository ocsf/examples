# Event Dossier: Mdatp Device Registry Events to OCSF class Win/registry Key Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_key_activity`
* Vendor name: `mdatp`
* Product name: `mdatp-device-registry-events`
* Event codes: `ACTION_TYPE ILIKE '%RegistryKey%'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'RegistryKeyCreated' THEN 1 WHEN ACTION_TYPE = 'RegistryKeyDeleted' THEN 4 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'RegistryKeyCreated' THEN 1 WHEN ACTION_TYPE = 'RegistryKeyDeleted' THEN 4 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 2 THEN 'Read' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Security' WHEN 7 THEN 'Restore' WHEN 8 THEN 'Import' WHEN 9 THEN 'Export' WHEN 99 THEN 'Other' END``` |
| actor.process.parent_process.cmd_line | ```INITIATING_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.parent_process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.created_time_dt | ```INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 ELSE 99 END::NUMBER, 'value', COALESCE(INITIATING_PROCESS_SHA1, INITIATING_PROCESS_MD5)::VARCHAR))``` |
| actor.process.parent_process.file.name | ```INITIATING_PROCESS_FILE_NAME::VARCHAR``` |
| actor.process.parent_process.file.parent_folder | ```INITIATING_PROCESS_FOLDER_PATH::VARCHAR``` |
| actor.process.parent_process.integrity | ```CASE (CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Untrusted' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'System' WHEN 6 THEN 'Protected' WHEN 99 THEN 'Other' END``` |
| actor.process.parent_process.integrity_id | ```CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 ELSE 99 END::NUMBER``` |
| actor.process.parent_process.parent_process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.parent_process.created_time_dt | ```INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.parent_process.file.name | ```INITIATING_PROCESS_PARENT_FILE_NAME::VARCHAR``` |
| actor.process.parent_process.parent_process.uid | ```INITIATING_PROCESS_PARENT_ID::VARCHAR``` |
| actor.process.parent_process.uid | ```INITIATING_PROCESS_ID::VARCHAR``` |
| actor.process.parent_process.user.account.name | ```INITIATING_PROCESS_ACCOUNT_NAME::VARCHAR``` |
| actor.process.parent_process.user.account.uid | ```INITIATING_PROCESS_ACCOUNT_SID::VARCHAR``` |
| actor.process.parent_process.user.domain | ```INITIATING_PROCESS_ACCOUNT_DOMAIN::VARCHAR``` |
| class_name | ```'win/registry_key_activity'``` |
| class_uid | ```201001``` |
| device.container.uid | ```APP_GUARD_CONTAINER_ID::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| metadata.product.name | ```'mdatp-device-registry-events'``` |
| metadata.product.vendor_name | ```'mdatp'``` |
| metadata.version | ```'1.1.0'``` |
| reg_key.path | ```REGISTRY_KEY::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((20100100 + (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'RegistryKeyCreated' THEN 1 WHEN ACTION_TYPE = 'RegistryKeyDeleted' THEN 4 ELSE 99 END))::NUMBER) WHEN 20100100 THEN 'Registry Key Activity: Unknown' WHEN 20100101 THEN 'Registry Key Activity: Create' WHEN 20100102 THEN 'Registry Key Activity: Read' WHEN 20100103 THEN 'Registry Key Activity: Modify' WHEN 20100104 THEN 'Registry Key Activity: Delete' WHEN 20100105 THEN 'Registry Key Activity: Rename' WHEN 20100106 THEN 'Registry Key Activity: Set Security' WHEN 20100107 THEN 'Registry Key Activity: Restore' WHEN 20100108 THEN 'Registry Key Activity: Import' WHEN 20100109 THEN 'Registry Key Activity: Export' WHEN 20100199 THEN 'Registry Key Activity: Other' END``` |
| type_uid | ```(20100100 + (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'RegistryKeyCreated' THEN 1 WHEN ACTION_TYPE = 'RegistryKeyDeleted' THEN 4 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
