# Event Dossier: Mdatp Device Network Events to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `mdatp`
* Product name: `mdatp-device-network-events`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION_TYPE ILIKE ANY ('%ConnectionSuccess%', '%ConnectionCreated%', '%ConnectionAccepted%', '%ConnectionFound%') THEN 1 WHEN ACTION_TYPE ILIKE '%ConnectionFailed%' THEN 2 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION_TYPE ILIKE ANY ('%ConnectionSuccess%', '%ConnectionCreated%', '%ConnectionAccepted%', '%ConnectionFound%') THEN 1 WHEN ACTION_TYPE ILIKE '%ConnectionFailed%' THEN 2 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN ACTION_TYPE ILIKE ANY ('%ConnectionSuccess%', '%ConnectionCreated%', '%ConnectionAccepted%', '%ConnectionFound%') THEN 1 WHEN ACTION_TYPE ILIKE '%ConnectionFailed%' THEN 4 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION_TYPE ILIKE ANY ('%ConnectionSuccess%', '%ConnectionCreated%', '%ConnectionAccepted%', '%ConnectionFound%') THEN 1 WHEN ACTION_TYPE ILIKE '%ConnectionFailed%' THEN 4 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```INITIATING_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.container.uid | ```APP_GUARD_CONTAINER_ID::VARCHAR``` |
| actor.process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.created_time_dt | ```INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(INITIATING_PROCESS_SHA1, INITIATING_PROCESS_MD5)::VARCHAR))``` |
| actor.process.file.name | ```INITIATING_PROCESS_FILE_NAME::VARCHAR``` |
| actor.process.file.path | ```INITIATING_PROCESS_FOLDER_PATH::VARCHAR``` |
| actor.process.integrity | ```CASE (CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Untrusted' THEN 1 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='System' THEN 5 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Protected' THEN 6 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Untrusted' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'System' WHEN 6 THEN 'Protected' WHEN 99 THEN 'Other' END``` |
| actor.process.integrity_id | ```CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Untrusted' THEN 1 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='System' THEN 5 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL='Protected' THEN 6 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| actor.process.parent_process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.created_time_dt | ```INITIATING_PROCESS_PARENT_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.name | ```INITIATING_PROCESS_PARENT_FILE_NAME::VARCHAR``` |
| actor.process.parent_process.pid | ```INITIATING_PROCESS_PARENT_ID::NUMBER``` |
| actor.process.pid | ```INITIATING_PROCESS_ID::NUMBER``` |
| actor.process.user.account.name | ```INITIATING_PROCESS_ACCOUNT_NAME::VARCHAR``` |
| actor.process.user.account.uid | ```INITIATING_PROCESS_ACCOUNT_SID::VARCHAR``` |
| actor.process.user.domain | ```INITIATING_PROCESS_ACCOUNT_DOMAIN::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| dst_endpoint.ip | ```REMOTE_IP::VARCHAR``` |
| dst_endpoint.port | ```REMOTE_PORT::NUMBER``` |
| metadata.product.name | ```'mdatp-device-network-events'``` |
| metadata.product.vendor_name | ```'mdatp'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```LOCAL_IP::VARCHAR``` |
| src_endpoint.port | ```LOCAL_PORT::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((400100 + (CASE WHEN ACTION_TYPE='ConnectionSuccess' THEN 1 WHEN ACTION_TYPE='ConnectionFailed' THEN 4 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END))::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```(400100 + (CASE WHEN ACTION_TYPE='ConnectionSuccess' THEN 1 WHEN ACTION_TYPE='ConnectionFailed' THEN 4 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
