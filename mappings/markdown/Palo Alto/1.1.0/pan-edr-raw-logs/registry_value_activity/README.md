# Event Dossier: Pan Edr Raw Logs to OCSF class Win/registry Value Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_value_activity`
* Vendor name: `paloalto`
* Product name: `pan-edr-raw-logs`
* Event codes: `EVENT_TYPE = 4 AND EVENT_SUB_TYPE IN (4, 5)`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 4 THEN 2 WHEN event_sub_type = 5 THEN 4 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 4 THEN 2 WHEN event_sub_type = 5 THEN 4 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Get' WHEN 2 THEN 'Set' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 99 THEN 'Other' END``` |
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
| class_name | ```'win/registry_value_activity'``` |
| class_uid | ```201002``` |
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
| reg_value.name | ```RAW:action_registry_value_name::VARCHAR``` |
| reg_value.path | ```RAW:action_registry_key_name::VARCHAR``` |
| reg_value.type | ```CASE (CASE WHEN RAW:action_registry_value_type IS NULL THEN 0 WHEN RAW:action_registry_value_type = 4 THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'REG_BINARY' WHEN 10 THEN 'REG_SZ' WHEN 2 THEN 'REG_DWORD' WHEN 3 THEN 'REG_DWORD_BIG_ENDIAN' WHEN 4 THEN 'REG_EXPAND_SZ' WHEN 5 THEN 'REG_LINK' WHEN 6 THEN 'REG_MULTI_SZ' WHEN 7 THEN 'REG_NONE' WHEN 8 THEN 'REG_QWORD' WHEN 9 THEN 'REG_QWORD_LITTLE_ENDIAN' WHEN 99 THEN 'Other' END``` |
| reg_value.type_id | ```CASE WHEN RAW:action_registry_value_type IS NULL THEN 0 WHEN RAW:action_registry_value_type = 4 THEN 2 ELSE 99 END::NUMBER``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```event_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((20100200 + (CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 4 THEN 2 WHEN event_sub_type = 5 THEN 4 ELSE 99 END))::NUMBER) WHEN 20100200 THEN 'Registry Value Activity: Unknown' WHEN 20100201 THEN 'Registry Value Activity: Get' WHEN 20100202 THEN 'Registry Value Activity: Set' WHEN 20100203 THEN 'Registry Value Activity: Modify' WHEN 20100204 THEN 'Registry Value Activity: Delete' WHEN 20100299 THEN 'Registry Value Activity: Other' END``` |
| type_uid | ```(20100200 + (CASE WHEN event_sub_type IS NULL THEN 0 WHEN event_sub_type = 4 THEN 2 WHEN event_sub_type = 5 THEN 4 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
