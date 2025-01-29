# Event Dossier: Beyondtrust Events to OCSF class Process Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `process_activity`
* Vendor name: `beyondtrust`
* Product name: `beyondtrust-events`
* Event codes: `EVENT_ACTION IN ('process-start-no-change', 'process-start-add-admin', 'process-start-cancelled-by-user', 'process-start-add-admin-on-demand', 'process-start-blocked', 'process-start-allowed')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN EVENT_ACTION is NULL AND EVENT_TYPE is NULL THEN 0 WHEN EVENT_ACTION = 'process-start-allowed' OR EVENT_TYPE[0] = 'allowed' THEN 1 WHEN EVENT_ACTION = 'process-start-blocked' OR EVENT_TYPE[0] = 'denied' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN EVENT_ACTION is NULL AND EVENT_TYPE is NULL THEN 0 WHEN EVENT_ACTION = 'process-start-allowed' OR EVENT_TYPE[0] = 'allowed' THEN 1 WHEN EVENT_ACTION = 'process-start-blocked' OR EVENT_TYPE[0] = 'denied' THEN 2 ELSE 99 END::NUMBER``` |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Launch' WHEN 2 THEN 'Terminate' WHEN 3 THEN 'Open' WHEN 4 THEN 'Inject' WHEN 5 THEN 'Set User ID' WHEN 99 THEN 'Other' END``` |
| actor.process.file.created_time | ```date_part('epoch_milliseconds', FILE:created::TIMESTAMP_LTZ)``` |
| actor.process.file.created_time_dt | ```FILE:created::TIMESTAMP_LTZ``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(FILE:hash:sha256 is NULL, IFF(FILE:hash:md5 is NULL, IFF(FILE:hash:sha1 is NULL, 0, 2), 1) , 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(FILE:hash:sha256 is NULL, IFF(FILE:hash:md5 is NULL, IFF(FILE:hash:sha1 is NULL, 0, 2), 1) , 3)::NUMBER, 'value', COALESCE(FILE:hash:sha256, COALESCE(FILE:hash:md5, COALESCE(FILE:hash:sha1, NULL)))::VARCHAR))``` |
| actor.process.file.name | ```FILE:name::VARCHAR``` |
| actor.process.file.owner.domain | ```FILE:Owner:DomainName::VARCHAR``` |
| actor.process.file.owner.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', FILE:group::VARCHAR, 'uid', FILE:gid::VARCHAR))``` |
| actor.process.file.owner.name | ```FILE:Owner:Name::VARCHAR``` |
| actor.process.file.parent_folder | ```FILE:directory::VARCHAR``` |
| actor.process.file.path | ```FILE:path::VARCHAR``` |
| actor.process.file.product.name | ```FILE:pe:product::VARCHAR``` |
| actor.process.file.product.version | ```FILE:pe:file_version::VARCHAR``` |
| actor.process.file.signature.certificate.subject | ```FILE:code_signature:subject_name::VARCHAR``` |
| actor.process.file.uid | ```FILE:uid::VARCHAR``` |
| actor.user.domain | ```USER:domain::VARCHAR``` |
| actor.user.name | ```USER:name::VARCHAR``` |
| actor.user.uid | ```USER:id::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'process_activity'``` |
| class_uid | ```1007``` |
| device.domain | ```HOST:domain::VARCHAR``` |
| device.hostname | ```HOST:hostname::VARCHAR``` |
| device.ip | ```HOST:ip[0]::VARCHAR``` |
| device.mac | ```HOST:mac[0]::VARCHAR``` |
| device.name | ```AGENT_NAME::VARCHAR``` |
| device.os.cpu_bits | ```CASE WHEN HOST:architecture = 'x64' THEN 64 WHEN HOST:architecture = 'x32' THEN 32 ELSE NULL END::NUMBER``` |
| device.os.name | ```HOST:os:name::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN HOST:os:type = 'windows' THEN 100 WHEN HOST:os:type = 'macos' THEN 300 WHEN HOST:os:type is NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN HOST:os:type = 'windows' THEN 100 WHEN HOST:os:type = 'macos' THEN 300 WHEN HOST:os:type is NULL THEN 0 ELSE 99 END::NUMBER``` |
| device.os.version | ```HOST:os:version::VARCHAR``` |
| device.type | ```CASE (CASE WHEN HOST:ChassisType = 'Laptop' THEN 3 WHEN HOST:ChassisType = 'Desktop' THEN 2 WHEN HOST:ChassisType is NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```CASE WHEN HOST:ChassisType = 'Laptop' THEN 3 WHEN HOST:ChassisType = 'Desktop' THEN 2 WHEN HOST:ChassisType is NULL THEN 0 ELSE 99 END::NUMBER``` |
| device.uid | ```AGENT_ID::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', EVENT_END::TIMESTAMP_LTZ)``` |
| end_time_dt | ```EVENT_END::TIMESTAMP_LTZ``` |
| message | ```EVENT_REASON::VARCHAR``` |
| metadata.product.name | ```'beyondtrust-events'``` |
| metadata.product.vendor_name | ```'beyondtrust'``` |
| metadata.version | ```'1.1.0'``` |
| process.cmd_line | ```PROCESS:command_line::VARCHAR``` |
| process.created_time | ```date_part('epoch_milliseconds', PROCESS:start::TIMESTAMP_LTZ)``` |
| process.created_time_dt | ```PROCESS:start::TIMESTAMP_LTZ``` |
| process.file.created_time | ```date_part('epoch_milliseconds', PROCESS:HostedFile:created::TIMESTAMP_LTZ)``` |
| process.file.created_time_dt | ```PROCESS:HostedFile:created::TIMESTAMP_LTZ``` |
| process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(PROCESS:HostedFile:hash IS NOT NULL, IFF(PROCESS:HostedFile:hash:sha256 is NULL, IFF(PROCESS:HostedFile:hash:md5 is NULL, IFF(PROCESS:HostedFile:hash:sha1 is NULL, 0, 2), 1) , 3), IFF(FILE:hash:sha256 is NULL, IFF(FILE:hash:md5 is NULL, IFF(FILE:hash:sha1 is NULL, 0, 2), 1) , 3))::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(PROCESS:HostedFile:hash IS NOT NULL, IFF(PROCESS:HostedFile:hash:sha256 is NULL, IFF(PROCESS:HostedFile:hash:md5 is NULL, IFF(PROCESS:HostedFile:hash:sha1 is NULL, 0, 2), 1) , 3), IFF(FILE:hash:sha256 is NULL, IFF(FILE:hash:md5 is NULL, IFF(FILE:hash:sha1 is NULL, 0, 2), 1) , 3))::NUMBER, 'value', IFF(PROCESS:HostedFile:hash IS NOT NULL, COALESCE(PROCESS:HostedFile:hash:sha256, COALESCE(PROCESS:HostedFile:hash:md5, COALESCE(PROCESS:HostedFile:hash:sha1, NULL))), COALESCE(FILE:hash:sha256, COALESCE(FILE:hash:md5, COALESCE(FILE:hash:sha1, NULL))))::VARCHAR))``` |
| process.file.name | ```COALESCE(PROCESS:HostedFile:name, FILE:name)::VARCHAR``` |
| process.file.owner.name | ```COALESCE(PROCESS:HostedFile:owner, FILE:Owner.Name)::VARCHAR``` |
| process.file.parent_folder | ```COALESCE(PROCESS:HostedFile:directory, FILE:directory)::VARCHAR``` |
| process.file.path | ```COALESCE(PROCESS:HostedFile:path, FILE:path)::VARCHAR``` |
| process.file.product.name | ```PROCESS:HostedFile:pe:product::VARCHAR``` |
| process.file.product.version | ```PROCESS:HostedFile:pe:file_version::VARCHAR``` |
| process.file.signature.certificate.subject | ```COALESCE(PROCESS:HostedFile:code_signature:subject_name, FILE:code_signature:subject_name)::VARCHAR``` |
| process.file.uid | ```COALESCE(PROCESS:HostedFile:uid, FILE:uid)::VARCHAR``` |
| process.file.version | ```COALESCE(PROCESS:HostedFile:ProductVersion, FILE:ProductVersion)::VARCHAR``` |
| process.name | ```PROCESS:name::VARCHAR``` |
| process.parent_process.cmd_line | ```PROCESS:parent:command_line::VARCHAR``` |
| process.parent_process.name | ```PROCESS:parent:name::VARCHAR``` |
| process.parent_process.pid | ```PROCESS:parent:pid::NUMBER``` |
| process.parent_process.uid | ```PROCESS:parent:entity_id::VARCHAR``` |
| process.pid | ```PROCESS:pid::NUMBER``` |
| process.uid | ```PROCESS:entity_id::VARCHAR``` |
| process.user.domain | ```PROCESS:user:domain::VARCHAR``` |
| process.user.name | ```PROCESS:user:name::VARCHAR``` |
| process.user.uid | ```PROCESS:user:id::VARCHAR``` |
| severity | ```CASE (IFF(EVENT_SEVERITY is NULL, 0, 99)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```IFF(EVENT_SEVERITY is NULL, 0, 99)::NUMBER``` |
| start_time | ```date_part('epoch_milliseconds', EVENT_START::TIMESTAMP_LTZ)``` |
| start_time_dt | ```EVENT_START::TIMESTAMP_LTZ``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (100799::NUMBER) WHEN 100700 THEN 'Process Activity: Unknown' WHEN 100701 THEN 'Process Activity: Launch' WHEN 100702 THEN 'Process Activity: Terminate' WHEN 100703 THEN 'Process Activity: Open' WHEN 100704 THEN 'Process Activity: Inject' WHEN 100705 THEN 'Process Activity: Set User ID' WHEN 100799 THEN 'Process Activity: Other' END``` |
| type_uid | ```100799::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
