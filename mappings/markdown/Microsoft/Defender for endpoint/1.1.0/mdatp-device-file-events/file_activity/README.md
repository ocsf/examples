# Event Dossier: Mdatp Device File Events to OCSF class File Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `file_activity`
* Vendor name: `mdatp`
* Product name: `mdatp-device-file-events`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE ACTION_TYPE WHEN 'FileCreated' THEN 1 WHEN 'FileModified' THEN 3 WHEN 'FileDeleted' THEN 4 WHEN 'FileRenamed' THEN 5 ELSE 0 END``` |
| activity_name | ```CASE (CASE ACTION_TYPE WHEN 'FileCreated' THEN 1 WHEN 'FileModified' THEN 3 WHEN 'FileDeleted' THEN 4 WHEN 'FileRenamed' THEN 5 ELSE 0 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 10 THEN 'Encrypt' WHEN 11 THEN 'Decrypt' WHEN 12 THEN 'Mount' WHEN 13 THEN 'Unmount' WHEN 14 THEN 'Open' WHEN 2 THEN 'Read' WHEN 3 THEN 'Update' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Attributes' WHEN 7 THEN 'Set Security' WHEN 8 THEN 'Get Attributes' WHEN 9 THEN 'Get Security' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```INITIATING_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.created_time_dt | ```INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.file.owner.account.name | ```INITIATING_PROCESS_ACCOUNT_NAME::VARCHAR``` |
| actor.process.file.owner.account.uid | ```INITIATING_PROCESS_ACCOUNT_SID::VARCHAR``` |
| actor.process.file.owner.domain | ```INITIATING_PROCESS_ACCOUNT_DOMAIN::VARCHAR``` |
| actor.process.file.owner.uid | ```INITIATING_PROCESS_ACCOUNT_SID::VARCHAR``` |
| actor.process.file.parent_folder | ```INITIATING_PROCESS_FOLDER_PATH::VARCHAR``` |
| actor.process.integrity | ```CASE (CASE INITIATING_PROCESS_INTEGRITY_LEVEL::VARCHAR WHEN 'Untrusted' THEN 1 WHEN 'Low' THEN 2 WHEN 'Medium' THEN 3 WHEN 'High' THEN 4 WHEN 'System' THEN 5 ELSE 0 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Untrusted' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'System' WHEN 6 THEN 'Protected' WHEN 99 THEN 'Other' END``` |
| actor.process.integrity_id | ```CASE INITIATING_PROCESS_INTEGRITY_LEVEL::VARCHAR WHEN 'Untrusted' THEN 1 WHEN 'Low' THEN 2 WHEN 'Medium' THEN 3 WHEN 'High' THEN 4 WHEN 'System' THEN 5 ELSE 0 END``` |
| actor.process.parent_process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.created_time_dt | ```INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.file.name | ```INITIATING_PROCESS_PARENT_FILE_NAME::VARCHAR``` |
| actor.process.parent_process.pid | ```INITIATING_PROCESS_PARENT_ID::NUMBER``` |
| actor.process.pid | ```INITIATING_PROCESS_ID::NUMBER``` |
| api.operation | ```OPERATION_NAME::VARCHAR``` |
| class_name | ```'file_activity'``` |
| class_uid | ```1001``` |
| device.container.uid | ```APP_GUARD_CONTAINER_ID::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| file.confidentiality | ```CASE (CASE WHEN SENSITIVITY_LABEL='Public' THEN 1 WHEN SENSITIVITY_LABEL='Confidential' THEN 2 WHEN SENSITIVITY_LABEL='Internal' THEN 3 WHEN SENSITIVITY_LABEL='Restricted' THEN 4 WHEN SENSITIVITY_LABEL IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Not Confidential' WHEN 2 THEN 'Confidential' WHEN 3 THEN 'Secret' WHEN 4 THEN 'Top Secret' WHEN 99 THEN 'Other' END``` |
| file.confidentiality_id | ```CASE WHEN SENSITIVITY_LABEL='Public' THEN 1 WHEN SENSITIVITY_LABEL='Confidential' THEN 2 WHEN SENSITIVITY_LABEL='Internal' THEN 3 WHEN SENSITIVITY_LABEL='Restricted' THEN 4 WHEN SENSITIVITY_LABEL IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| file.created_time | ```date_part('epoch_milliseconds', TIMESTAMP::TIMESTAMP_LTZ)``` |
| file.created_time_dt | ```TIMESTAMP::TIMESTAMP_LTZ``` |
| file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN MD5 is not null THEN 1 WHEN SHA1 is not null THEN 2 WHEN SHA256 is not null THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN MD5 is not null THEN 1 WHEN SHA1 is not null THEN 2 WHEN SHA256 is not null THEN 3 ELSE 99 END::NUMBER))``` |
| file.name | ```FILE_NAME::VARCHAR``` |
| file.path | ```FOLDER_PATH::VARCHAR``` |
| metadata.product.name | ```'mdatp-device-file-events'``` |
| metadata.product.vendor_name | ```'mdatp'``` |
| metadata.version | ```'1.1.0'``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE ACTION_TYPE WHEN 'FileCreated' THEN 100101 WHEN 'FileModified' THEN 100103 WHEN 'FileDeleted' THEN 100104 WHEN 'FileRenamed' THEN 100105 ELSE 100100 END) WHEN 100100 THEN 'File System Activity: Unknown' WHEN 100101 THEN 'File System Activity: Create' WHEN 100102 THEN 'File System Activity: Read' WHEN 100103 THEN 'File System Activity: Update' WHEN 100104 THEN 'File System Activity: Delete' WHEN 100105 THEN 'File System Activity: Rename' WHEN 100106 THEN 'File System Activity: Set Attributes' WHEN 100107 THEN 'File System Activity: Set Security' WHEN 100108 THEN 'File System Activity: Get Attributes' WHEN 100109 THEN 'File System Activity: Get Security' WHEN 100110 THEN 'File System Activity: Encrypt' WHEN 100111 THEN 'File System Activity: Decrypt' WHEN 100112 THEN 'File System Activity: Mount' WHEN 100113 THEN 'File System Activity: Unmount' WHEN 100114 THEN 'File System Activity: Open' WHEN 100199 THEN 'File System Activity: Other' END``` |
| type_uid | ```CASE ACTION_TYPE WHEN 'FileCreated' THEN 100101 WHEN 'FileModified' THEN 100103 WHEN 'FileDeleted' THEN 100104 WHEN 'FileRenamed' THEN 100105 ELSE 100100 END``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
