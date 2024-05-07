# Event Dossier: Pan Edr Raw Logs to OCSF class Process Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `process_activity`
* Vendor name: `paloalto`
* Product name: `pan-edr-raw-logs`
* Event codes: `EVENT_TYPE = 1`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN event_sub_type is null THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 2 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN event_sub_type is null THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Launch' WHEN 2 THEN 'Terminate' WHEN 3 THEN 'Open' WHEN 4 THEN 'Inject' WHEN 5 THEN 'Set User ID' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```OS_ACTOR_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 0 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 99 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 0 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 99 end::NUMBER, 'value', COALESCE(OS_ACTOR_PROCESS_IMAGE_SHA256, OS_ACTOR_PROCESS_IMAGE_MD5)::VARCHAR))``` |
| actor.process.file.name | ```OS_ACTOR_PROCESS_IMAGE_NAME::VARCHAR``` |
| actor.process.file.path | ```OS_ACTOR_PROCESS_IMAGE_PATH::VARCHAR``` |
| actor.process.pid | ```OS_ACTOR_PROCESS_OS_PID::NUMBER``` |
| actor.process.tid | ```OS_ACTOR_THREAD_THREAD_ID::NUMBER``` |
| actor.process.user.name | ```OS_ACTOR_PRIMARY_USERNAME::VARCHAR``` |
| actor.process.user.uid | ```OS_ACTOR_PRIMARY_USER_SID::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'process_activity'``` |
| class_uid | ```1007``` |
| device.hostname | ```AGENT_HOSTNAME::VARCHAR``` |
| device.ip | ```COALESCE(AGENT_IP_ADDRESSES[0], AGENT_IP_ADDRESSES_V6[0])::VARCHAR``` |
| device.mac | ```AGENT_INTERFACE_MAP_MAC[0]::VARCHAR``` |
| device.os.type | ```CASE (case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER``` |
| device.os.version | ```AGENT_OS_SUB_TYPE::VARCHAR``` |
| device.uid | ```AGENT_ID::VARCHAR``` |
| metadata.product.name | ```'pan-edr-raw-logs'``` |
| metadata.product.vendor_name | ```'paloalto'``` |
| metadata.version | ```'1.1.0'``` |
| process.cmd_line | ```ACTION_PROCESS_IMAGE_COMMAND_LINE::VARCHAR``` |
| process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN ACTION_PROCESS_IMAGE_SHA256 IS NULL AND ACTION_PROCESS_IMAGE_MD5 IS NULL THEN 0 WHEN ACTION_PROCESS_IMAGE_SHA256 IS NOT NULL THEN 3 WHEN ACTION_PROCESS_IMAGE_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN ACTION_PROCESS_IMAGE_SHA256 IS NULL AND ACTION_PROCESS_IMAGE_MD5 IS NULL THEN 0 WHEN ACTION_PROCESS_IMAGE_SHA256 IS NOT NULL THEN 3 WHEN ACTION_PROCESS_IMAGE_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(ACTION_PROCESS_IMAGE_SHA256, ACTION_PROCESS_IMAGE_MD5)::VARCHAR))``` |
| process.file.name | ```ACTION_PROCESS_IMAGE_NAME::VARCHAR``` |
| process.file.path | ```ACTION_PROCESS_IMAGE_PATH::VARCHAR``` |
| process.pid | ```ACTION_PROCESS_OS_PID::NUMBER``` |
| process.terminated_time | ```date_part('epoch_milliseconds', ACTION_PROCESS_TERMINATION_DATE::TIMESTAMP_LTZ)``` |
| process.terminated_time_dt | ```ACTION_PROCESS_TERMINATION_DATE::TIMESTAMP_LTZ``` |
| process.user.name | ```ACTION_PROCESS_USERNAME::VARCHAR``` |
| process.user.uid | ```ACTION_PROCESS_USER_SID::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```event_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((100700 + (CASE WHEN event_sub_type is null THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 2 ELSE 99 END))::NUMBER) WHEN 100700 THEN 'Process Activity: Unknown' WHEN 100701 THEN 'Process Activity: Launch' WHEN 100702 THEN 'Process Activity: Terminate' WHEN 100703 THEN 'Process Activity: Open' WHEN 100704 THEN 'Process Activity: Inject' WHEN 100705 THEN 'Process Activity: Set User ID' WHEN 100799 THEN 'Process Activity: Other' END``` |
| type_uid | ```(100700 + (CASE WHEN event_sub_type is null THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 2 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
