# Event Dossier: Mdatp Device Logon Events to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `mdatp`
* Product name: `mdatp-device-logon-events`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'LogonSuccess' THEN 1 WHEN ACTION_TYPE = 'LogonFailed' THEN 2 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'LogonSuccess' THEN 1 WHEN ACTION_TYPE = 'LogonFailed' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```INITIATING_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.created_time | ```date_part('epoch_milliseconds', INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ)``` |
| actor.process.created_time_dt | ```INITIATING_PROCESS_CREATION_TIME::TIMESTAMP_LTZ``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (CASE WHEN INITIATING_PROCESS_SHA256 IS NULL AND INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA256 IS NOT NULL THEN 3 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', CASE WHEN INITIATING_PROCESS_SHA256 IS NULL AND INITIATING_PROCESS_SHA1 IS NULL AND INITIATING_PROCESS_MD5 IS NULL THEN 0 WHEN INITIATING_PROCESS_SHA256 IS NOT NULL THEN 3 WHEN INITIATING_PROCESS_SHA1 IS NOT NULL THEN 2 WHEN INITIATING_PROCESS_MD5 IS NOT NULL THEN 1 END::NUMBER, 'value', COALESCE(INITIATING_PROCESS_SHA256, INITIATING_PROCESS_SHA1, INITIATING_PROCESS_MD5)::VARCHAR))``` |
| actor.process.file.name | ```INITIATING_PROCESS_FILE_NAME::VARCHAR``` |
| actor.process.file.path | ```INITIATING_PROCESS_FOLDER_PATH::VARCHAR``` |
| actor.process.integrity | ```CASE (CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Untrusted' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'System' WHEN 6 THEN 'Protected' WHEN 99 THEN 'Other' END``` |
| actor.process.integrity_id | ```CASE WHEN INITIATING_PROCESS_INTEGRITY_LEVEL IS NULL THEN 0 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Low' THEN 2 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'Medium' THEN 3 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'High' THEN 4 WHEN INITIATING_PROCESS_INTEGRITY_LEVEL = 'System' THEN 5 ELSE 99 END::NUMBER``` |
| actor.process.parent_process.file.name | ```INITIATING_PROCESS_PARENT_FILE_NAME::VARCHAR``` |
| actor.process.parent_process.pid | ```INITIATING_PROCESS_PARENT_ID::NUMBER``` |
| actor.process.pid | ```INITIATING_PROCESS_ID::NUMBER``` |
| actor.process.user.account.name | ```INITIATING_PROCESS_ACCOUNT_NAME::VARCHAR``` |
| actor.process.user.account.uid | ```INITIATING_PROCESS_ACCOUNT_SID::VARCHAR``` |
| actor.process.user.domain | ```INITIATING_PROCESS_ACCOUNT_DOMAIN::VARCHAR``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| device.container.uid | ```APP_GUARD_CONTAINER_ID::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| is_remote | ```REMOTE_IP IS NOT NULL``` |
| logon_process.uid | ```LOGON_ID::VARCHAR``` |
| logon_type | ```CASE (CASE WHEN LOGON_TYPE = 'Interactive' THEN 2 WHEN LOGON_TYPE = 'Network' THEN 3 WHEN LOGON_TYPE = 'Batch' THEN 4 WHEN LOGON_TYPE = 'Unlock' THEN 7 WHEN LOGON_TYPE = 'NetworkCleartext' THEN 8 WHEN LOGON_TYPE = 'NewCredentials' THEN 9 WHEN LOGON_TYPE = 'RemoteInteractive' THEN 10 WHEN LOGON_TYPE = 'CachedInteractive' THEN 11 WHEN LOGON_TYPE = 'CachedRemoteInteractive' THEN 12 ELSE 99 END::NUMBER) WHEN 0 THEN 'System' WHEN 10 THEN 'Remote Interactive' WHEN 11 THEN 'Cached Interactive' WHEN 12 THEN 'Cached Remote Interactive' WHEN 13 THEN 'Cached Unlock' WHEN 2 THEN 'Interactive' WHEN 3 THEN 'Network' WHEN 4 THEN 'Batch' WHEN 5 THEN 'OS Service' WHEN 7 THEN 'Unlock' WHEN 8 THEN 'Network Cleartext' WHEN 9 THEN 'New Credentials' WHEN 99 THEN 'Other' END``` |
| logon_type_id | ```CASE WHEN LOGON_TYPE = 'Interactive' THEN 2 WHEN LOGON_TYPE = 'Network' THEN 3 WHEN LOGON_TYPE = 'Batch' THEN 4 WHEN LOGON_TYPE = 'Unlock' THEN 7 WHEN LOGON_TYPE = 'NetworkCleartext' THEN 8 WHEN LOGON_TYPE = 'NewCredentials' THEN 9 WHEN LOGON_TYPE = 'RemoteInteractive' THEN 10 WHEN LOGON_TYPE = 'CachedInteractive' THEN 11 WHEN LOGON_TYPE = 'CachedRemoteInteractive' THEN 12 ELSE 99 END::NUMBER``` |
| metadata.product.name | ```'mdatp-device-logon-events'``` |
| metadata.product.vendor_name | ```'mdatp'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.hostname | ```REMOTE_DEVICE_NAME::VARCHAR``` |
| src_endpoint.ip | ```REMOTE_IP::VARCHAR``` |
| src_endpoint.port | ```REMOTE_PORT::VARCHAR``` |
| status | ```CASE (CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'LogonSuccess' THEN 1 WHEN ACTION_TYPE = 'LogonFailed' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'LogonSuccess' THEN 1 WHEN ACTION_TYPE = 'LogonFailed' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((300200 +(CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'LogonSuccess' THEN 1 WHEN ACTION_TYPE = 'LogonFailed' THEN 2 ELSE 99 END))::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```(300200 +(CASE WHEN ACTION_TYPE IS NULL THEN 0 WHEN ACTION_TYPE = 'LogonSuccess' THEN 1 WHEN ACTION_TYPE = 'LogonFailed' THEN 2 ELSE 99 END))::NUMBER``` |
| user.domain | ```ACCOUNT_DOMAIN::VARCHAR``` |
| user.name | ```ACCOUNT_NAME::VARCHAR``` |
| user.uid | ```ACCOUNT_SID::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
