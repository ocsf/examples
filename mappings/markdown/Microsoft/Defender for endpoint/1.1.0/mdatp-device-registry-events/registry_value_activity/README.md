# Event Dossier: Mdatp Device Registry Events to OCSF class Win/registry Value Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_value_activity`
* Vendor name: `mdatp`
* Product name: `mdatp-device-registry-events`
* Event codes: `ACTION_TYPE ILIKE '%RegistryValue%'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'RegistryValueSet' then 2 WHEN ACTION_TYPE = 'RegistryValueDeleted' then 4 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'RegistryValueSet' then 2 WHEN ACTION_TYPE = 'RegistryValueDeleted' then 4 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Get' WHEN 2 THEN 'Set' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```INITIATING_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.created_time_dt | ```INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(INITIATING_PROCESS_MD5 IS NULL, IFF(INITIATING_PROCESS_SHA1 IS NULL, 0, 2), 1)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(INITIATING_PROCESS_MD5 IS NULL, IFF(INITIATING_PROCESS_SHA1 IS NULL, 0, 2), 1)::NUMBER, 'value', COALESCE(INITIATING_PROCESS_MD5, INITIATING_PROCESS_SHA1)::VARCHAR))``` |
| actor.process.file.name | ```INITIATING_PROCESS_FILE_NAME::VARCHAR``` |
| actor.process.file.parent_folder | ```INITIATING_PROCESS_FOLDER_PATH::VARCHAR``` |
| actor.process.integrity | ```CASE (CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Untrusted' THEN 1 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Untrusted' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'System' WHEN 6 THEN 'Protected' WHEN 99 THEN 'Other' END``` |
| actor.process.integrity_id | ```CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Untrusted' THEN 1 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER``` |
| actor.process.parent_process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.created_time_dt | ```INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.file.name | ```INITIATING_PROCESS_PARENT_FILE_NAME::VARCHAR``` |
| actor.process.parent_process.uid | ```INITIATING_PROCESS_PARENT_ID::VARCHAR``` |
| actor.process.uid | ```INITIATING_PROCESS_ID::VARCHAR``` |
| actor.process.user.account.name | ```INITIATING_PROCESS_ACCOUNT_NAME::VARCHAR``` |
| actor.process.user.account.uid | ```INITIATING_PROCESS_ACCOUNT_SID::VARCHAR``` |
| actor.process.user.domain | ```INITIATING_PROCESS_ACCOUNT_DOMAIN::VARCHAR``` |
| api.operation | ```OPERATION_NAME::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'win/registry_value_activity'``` |
| class_uid | ```201002``` |
| device.container.uid | ```APP_GUARD_CONTAINER_ID::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| disposition | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```99::NUMBER``` |
| metadata.product.name | ```'mdatp-device-registry-events'``` |
| metadata.product.vendor_name | ```'mdatp'``` |
| metadata.version | ```'1.1.0'``` |
| prev_reg_value.name | ```PREVIOUS_REGISTRY_VALUE_NAME::VARCHAR``` |
| reg_value.name | ```REGISTRY_VALUE_NAME::VARCHAR``` |
| reg_value.path | ```REGISTRY_KEY::VARCHAR``` |
| reg_value.type | ```CASE (CASE WHEN REGISTRY_VALUE_TYPE IS NULL THEN 0 WHEN REGISTRY_VALUE_TYPE = 'Binary' THEN 1 WHEN REGISTRY_VALUE_TYPE = 'Dword' THEN 2 WHEN REGISTRY_VALUE_TYPE = 'ExpandString' THEN 4 WHEN REGISTRY_VALUE_TYPE = 'Link' THEN 5 WHEN REGISTRY_VALUE_TYPE = 'MultiString' THEN 6 WHEN REGISTRY_VALUE_TYPE = 'None' THEN 7 WHEN REGISTRY_VALUE_TYPE = 'Qword' THEN 8 WHEN REGISTRY_VALUE_TYPE = 'String' THEN 10 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'REG_BINARY' WHEN 10 THEN 'REG_SZ' WHEN 2 THEN 'REG_DWORD' WHEN 3 THEN 'REG_DWORD_BIG_ENDIAN' WHEN 4 THEN 'REG_EXPAND_SZ' WHEN 5 THEN 'REG_LINK' WHEN 6 THEN 'REG_MULTI_SZ' WHEN 7 THEN 'REG_NONE' WHEN 8 THEN 'REG_QWORD' WHEN 9 THEN 'REG_QWORD_LITTLE_ENDIAN' WHEN 99 THEN 'Other' END``` |
| reg_value.type_id | ```CASE WHEN REGISTRY_VALUE_TYPE IS NULL THEN 0 WHEN REGISTRY_VALUE_TYPE = 'Binary' THEN 1 WHEN REGISTRY_VALUE_TYPE = 'Dword' THEN 2 WHEN REGISTRY_VALUE_TYPE = 'ExpandString' THEN 4 WHEN REGISTRY_VALUE_TYPE = 'Link' THEN 5 WHEN REGISTRY_VALUE_TYPE = 'MultiString' THEN 6 WHEN REGISTRY_VALUE_TYPE = 'None' THEN 7 WHEN REGISTRY_VALUE_TYPE = 'Qword' THEN 8 WHEN REGISTRY_VALUE_TYPE = 'String' THEN 10 ELSE 99 END::NUMBER``` |
| severity | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```99::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN ACTION_TYPE IS NULL THEN 20100200 WHEN ACTION_TYPE = 'RegistryValueSet' then 20100202 WHEN ACTION_TYPE = 'RegistryValueDeleted' then 20100204 ELSE 20100299 END::NUMBER) WHEN 20100200 THEN 'Registry Value Activity: Unknown' WHEN 20100201 THEN 'Registry Value Activity: Get' WHEN 20100202 THEN 'Registry Value Activity: Set' WHEN 20100203 THEN 'Registry Value Activity: Modify' WHEN 20100204 THEN 'Registry Value Activity: Delete' WHEN 20100299 THEN 'Registry Value Activity: Other' END``` |
| type_uid | ```CASE WHEN ACTION_TYPE IS NULL THEN 20100200 WHEN ACTION_TYPE = 'RegistryValueSet' then 20100202 WHEN ACTION_TYPE = 'RegistryValueDeleted' then 20100204 ELSE 20100299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
