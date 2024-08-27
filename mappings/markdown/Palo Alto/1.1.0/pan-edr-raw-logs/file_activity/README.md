# Event Dossier: Pan Edr Raw Logs to OCSF class File Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `file_activity`
* Vendor name: `paloalto`
* Product name: `pan-edr-raw-logs`
* Event codes: `event_type = 3`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0:NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0:NUMBER``` |
| actor.process.cmd_line | ```OS_ACTOR_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 1 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 0 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 1 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 0 end::NUMBER, 'value', COALESCE(OS_ACTOR_PROCESS_IMAGE_SHA256, OS_ACTOR_PROCESS_IMAGE_MD5)::VARCHAR))``` |
| actor.process.file.name | ```OS_ACTOR_PROCESS_IMAGE_NAME::VARCHAR``` |
| actor.process.file.path | ```OS_ACTOR_PROCESS_IMAGE_PATH::VARCHAR``` |
| actor.process.pid | ```OS_ACTOR_PROCESS_OS_PID::NUMBER``` |
| actor.process.tid | ```OS_ACTOR_THREAD_THREAD_ID::NUMBER``` |
| actor.process.user.name | ```OS_ACTOR_PRIMARY_USERNAME::VARCHAR``` |
| actor.process.user.uid | ```OS_ACTOR_PRIMARY_USER_SID::VARCHAR``` |
| class_name | ```'file_activity'``` |
| class_uid | ```1001``` |
| device.hostname | ```AGENT_HOSTNAME::VARCHAR``` |
| device.ip | ```COALESCE(AGENT_IP_ADDRESSES[0], AGENT_IP_ADDRESSES_V6[0])::VARCHAR``` |
| device.mac | ```AGENT_INTERFACE_MAP_MAC[0]::VARCHAR``` |
| device.os.type | ```CASE (case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER``` |
| device.os.version | ```AGENT_OS_SUB_TYPE::VARCHAR``` |
| device.subnet | ```COALESCE(raw:agent_interface_map[0]:ipv4_subnet_mask, raw:agent_interface_map[0]:ipv6_subnet_mask)::VARCHAR``` |
| device.uid | ```AGENT_ID::VARCHAR``` |
| file.accessed_time | ```date_part('epoch_milliseconds', ACTION_FILE_ACCESS_TIME::TIMESTAMP_LTZ)``` |
| file.accessed_time_dt | ```ACTION_FILE_ACCESS_TIME::TIMESTAMP_LTZ``` |
| file.created_time | ```date_part('epoch_milliseconds', ACTION_FILE_CREATE_TIME::TIMESTAMP_LTZ)``` |
| file.created_time_dt | ```ACTION_FILE_CREATE_TIME::TIMESTAMP_LTZ``` |
| file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (case when ACTION_FILE_SHA256 is null and ACTION_FILE_MD5 is null then 1 when ACTION_FILE_SHA256 is not null then 3 when ACTION_FILE_MD5 is not null then 1 else 0 end::NUMBER ::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', case when ACTION_FILE_SHA256 is null and ACTION_FILE_MD5 is null then 1 when ACTION_FILE_SHA256 is not null then 3 when ACTION_FILE_MD5 is not null then 1 else 0 end::NUMBER ::NUMBER))``` |
| file.modified_time | ```date_part('epoch_milliseconds', ACTION_FILE_MOD_TIME::TIMESTAMP_LTZ)``` |
| file.modified_time_dt | ```ACTION_FILE_MOD_TIME::TIMESTAMP_LTZ``` |
| file.name | ```ACTION_FILE_NAME::VARCHAR``` |
| file.owner.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', ACTION_FILE_GROUP_NAME::VARCHAR, 'uid', ACTION_FILE_GROUP::VARCHAR))``` |
| file.owner.name | ```ACTION_FILE_OWNER_NAME::VARCHAR``` |
| file.owner.uid | ```ACTION_FILE_OWNER::VARCHAR``` |
| file.path | ```ACTION_FILE_PATH::VARCHAR``` |
| file.size | ```ACTION_FILE_SIZE::NUMBER``` |
| file.type | ```CASE (case when ACTION_FILE_DEVICE_TYPE = 0 then 0 when ACTION_FILE_DEVICE_TYPE = 1 then 6 else 0 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Regular File' WHEN 2 THEN 'Folder' WHEN 3 THEN 'Character Device' WHEN 4 THEN 'Block Device' WHEN 5 THEN 'Local Socket' WHEN 6 THEN 'Named Pipe' WHEN 7 THEN 'Symbolic Link' WHEN 99 THEN 'Other' END``` |
| file.type_id | ```case when ACTION_FILE_DEVICE_TYPE = 0 then 0 when ACTION_FILE_DEVICE_TYPE = 1 then 6 else 0 end::NUMBER``` |
| metadata.product.name | ```'pan-edr-raw-logs'``` |
| metadata.product.vendor_name | ```'paloalto'``` |
| metadata.version | ```'1.1.0'``` |
| time | ```date_part('epoch_milliseconds', event_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```event_timestamp::TIMESTAMP_LTZ``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
