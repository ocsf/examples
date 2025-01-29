# Event Dossier: Cb Platform Events to OCSF class File Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `file_activity`
* Vendor name: `cb-defense`
* Product name: `cb-platform-events`
* Event codes: `TYPE LIKE '%file%'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 10 THEN 'Encrypt' WHEN 11 THEN 'Decrypt' WHEN 12 THEN 'Mount' WHEN 13 THEN 'Unmount' WHEN 14 THEN 'Open' WHEN 2 THEN 'Read' WHEN 3 THEN 'Update' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Attributes' WHEN 7 THEN 'Set Security' WHEN 8 THEN 'Get Attributes' WHEN 9 THEN 'Get Security' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```PROCESS_CMDLINE::VARCHAR``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (3::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', 3::NUMBER, 'value', PROCESS_HASH_SHA256::VARCHAR))``` |
| actor.process.file.owner.org.uid | ```ORG_KEY::VARCHAR``` |
| actor.process.file.path | ```PROCESS_PATH::VARCHAR``` |
| actor.process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (3::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', 3::NUMBER, 'value', PARENT_HASH_SHA256::VARCHAR))``` |
| actor.process.parent_process.file.path | ```PARENT_PATH::VARCHAR``` |
| actor.process.parent_process.pid | ```PARENT_PID::NUMBER``` |
| actor.process.parent_process.uid | ```PARENT_GUID::VARCHAR``` |
| actor.process.pid | ```PROCESS_PID::NUMBER``` |
| actor.process.uid | ```PROCESS_GUID::VARCHAR``` |
| actor.user.name | ```PROCESS_USERNAME::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'file_activity'``` |
| class_uid | ```1001``` |
| device.created_time | ```date_part('epoch_milliseconds', DEVICE_TIMESTAMP::TIMESTAMP_LTZ)``` |
| device.created_time_dt | ```DEVICE_TIMESTAMP::TIMESTAMP_LTZ``` |
| device.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', DEVICE_GROUP::VARCHAR))``` |
| device.ip | ```DEVICE_EXTERNAL_IP::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.os.name | ```DEVICE_OS::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (3::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', 3::NUMBER, 'value', FILEMOD_HASH_SHA256::VARCHAR))``` |
| file.modifier.name | ```FILEMOD_NAME::VARCHAR``` |
| message | ```EVENT_DESCRIPTION::VARCHAR``` |
| metadata.event_code | ```type``` |
| metadata.product.name | ```'cb-platform-events'``` |
| metadata.product.vendor_name | ```'cb-defense'``` |
| metadata.version | ```'1.1.0'``` |
| time | ```date_part('epoch_milliseconds', backend_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```backend_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (100199::NUMBER) WHEN 100100 THEN 'File System Activity: Unknown' WHEN 100101 THEN 'File System Activity: Create' WHEN 100102 THEN 'File System Activity: Read' WHEN 100103 THEN 'File System Activity: Update' WHEN 100104 THEN 'File System Activity: Delete' WHEN 100105 THEN 'File System Activity: Rename' WHEN 100106 THEN 'File System Activity: Set Attributes' WHEN 100107 THEN 'File System Activity: Set Security' WHEN 100108 THEN 'File System Activity: Get Attributes' WHEN 100109 THEN 'File System Activity: Get Security' WHEN 100110 THEN 'File System Activity: Encrypt' WHEN 100111 THEN 'File System Activity: Decrypt' WHEN 100112 THEN 'File System Activity: Mount' WHEN 100113 THEN 'File System Activity: Unmount' WHEN 100114 THEN 'File System Activity: Open' WHEN 100199 THEN 'File System Activity: Other' END``` |
| type_uid | ```100199::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
