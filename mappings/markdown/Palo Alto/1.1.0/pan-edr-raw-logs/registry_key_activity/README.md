# Event Dossier: Pan Edr Raw Logs to OCSF class Win/registry Key Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_key_activity`
* Vendor name: `paloalto`
* Product name: `pan-edr-raw-logs`
* Event codes: `EVENT_TYPE = 4 AND EVENT_SUB_TYPE IN (1, 2, 3)`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 4 WHEN event_sub_type = 3 THEN 5 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 4 WHEN event_sub_type = 3 THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 2 THEN 'Read' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Security' WHEN 7 THEN 'Restore' WHEN 8 THEN 'Import' WHEN 9 THEN 'Export' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```OS_ACTOR_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 0 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 99 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 0 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 99 end::NUMBER, 'value', COALESCE(OS_ACTOR_PROCESS_IMAGE_SHA256, OS_ACTOR_PROCESS_IMAGE_MD5)::VARCHAR))``` |
| actor.process.file.name | ```OS_ACTOR_PROCESS_IMAGE_NAME::VARCHAR``` |
| actor.process.file.path | ```OS_ACTOR_PROCESS_IMAGE_PATH::VARCHAR``` |
| actor.process.pid | ```OS_ACTOR_PROCESS_OS_PID::NUMBER``` |
| actor.process.tid | ```OS_ACTOR_THREAD_THREAD_ID::NUMBER``` |
| actor.user.name | ```OS_ACTOR_PRIMARY_USERNAME::VARCHAR``` |
| actor.user.uid | ```OS_ACTOR_PRIMARY_USER_SID::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'win/registry_key_activity'``` |
| class_uid | ```201001``` |
| device.hostname | ```AGENT_HOSTNAME::VARCHAR``` |
| device.ip | ```COALESCE(AGENT_IP_ADDRESSES[0], AGENT_IP_ADDRESSES_V6[0])::VARCHAR``` |
| device.mac | ```AGENT_INTERFACE_MAP_MAC[0]::VARCHAR``` |
| device.os.type | ```CASE (case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER``` |
| device.os.version | ```AGENT_OS_SUB_TYPE::VARCHAR``` |
| device.uid | ```AGENT_ID::VARCHAR``` |
| disposition | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```99::NUMBER``` |
| metadata.product.name | ```'pan-edr-raw-logs'``` |
| metadata.product.vendor_name | ```'paloalto'``` |
| metadata.version | ```'1.1.0'``` |
| reg_key.path | ```RAW:action_registry_key_name::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```event_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((20100100 + (CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 4 WHEN event_sub_type = 3 THEN 5 ELSE 99 END))::NUMBER) WHEN 20100100 THEN 'Registry Key Activity: Unknown' WHEN 20100101 THEN 'Registry Key Activity: Create' WHEN 20100102 THEN 'Registry Key Activity: Read' WHEN 20100103 THEN 'Registry Key Activity: Modify' WHEN 20100104 THEN 'Registry Key Activity: Delete' WHEN 20100105 THEN 'Registry Key Activity: Rename' WHEN 20100106 THEN 'Registry Key Activity: Set Security' WHEN 20100107 THEN 'Registry Key Activity: Restore' WHEN 20100108 THEN 'Registry Key Activity: Import' WHEN 20100109 THEN 'Registry Key Activity: Export' WHEN 20100199 THEN 'Registry Key Activity: Other' END``` |
| type_uid | ```(20100100 + (CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 1 THEN 1 WHEN event_sub_type = 2 THEN 4 WHEN event_sub_type = 3 THEN 5 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
