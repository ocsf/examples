# Event Dossier: Sentinelone Raw Events V2 to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `sentinelone`
* Product name: `sentinelone-raw-events-v2`
* Event codes: `EVENT_TYPE IN ('IP Listen', 'IP Connect')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```SRC_PROCESS_CMDLINE::VARCHAR``` |
| actor.process.container.image.path | ```SRC_PROCESS_IMAGE_PATH::VARCHAR``` |
| actor.process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_START_TIME::TIMESTAMP_LTZ)``` |
| actor.process.created_time_dt | ```SRC_PROCESS_START_TIME::TIMESTAMP_LTZ``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(SRC_PROCESS_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(SRC_PROCESS_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER, 'value', SRC_PROCESS_IMAGE_SHA256::VARCHAR))``` |
| actor.process.parent_process.cmd_line | ```SRC_PROCESS_PARENT_CMDLINE::VARCHAR``` |
| actor.process.parent_process.created_time | ```date_part('epoch_milliseconds', SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ)``` |
| actor.process.parent_process.created_time_dt | ```SRC_PROCESS_PARENT_START_TIME::TIMESTAMP_LTZ``` |
| actor.process.parent_process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (IFF(SRC_PROCESS_PARENT_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', IFF(SRC_PROCESS_PARENT_IMAGE_SHA256 IS NULL, 0, 3)::NUMBER, 'value', SRC_PROCESS_PARENT_IMAGE_SHA256::VARCHAR))``` |
| actor.process.parent_process.name | ```SRC_PROCESS_PARENT_NAME::VARCHAR``` |
| actor.process.parent_process.pid | ```SRC_PROCESS_PARENT_PID::NUMBER``` |
| actor.process.parent_process.uid | ```SRC_PROCESS_PARENT_UID::VARCHAR``` |
| actor.process.pid | ```SRC_PROCESS_PID::NUMBER``` |
| actor.process.uid | ```SRC_PROCESS_UID::VARCHAR``` |
| actor.process.user.name | ```SRC_PROCESS_USER_NAME::VARCHAR``` |
| actor.session.uid | ```LOGIN_USER_SID::VARCHAR``` |
| actor.user.name | ```LOGIN_USER_NAME::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.direction | ```CASE (CASE WHEN DIRECTION IS NULL THEN 0 WHEN DIRECTION = 'INCOMING' THEN 1 WHEN DIRECTION = 'OUTGOING' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```CASE WHEN DIRECTION IS NULL THEN 0 WHEN DIRECTION = 'INCOMING' THEN 1 WHEN DIRECTION = 'OUTGOING' THEN 2 ELSE 99 END::NUMBER``` |
| connection_info.protocol_name | ```RAW:"event.network.protocolName"::VARCHAR``` |
| device.name | ```COMPUTER_NAME::VARCHAR``` |
| device.os.name | ```OS_NAME::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN OS_FAMILY IS NULL THEN 0 WHEN OS_FAMILY = 'windows' THEN 100 WHEN OS_FAMILY = 'linux' THEN 200 WHEN OS_FAMILY = 'osx' THEN 300 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS_FAMILY IS NULL THEN 0 WHEN OS_FAMILY = 'windows' THEN 100 WHEN OS_FAMILY = 'linux' THEN 200 WHEN OS_FAMILY = 'osx' THEN 300 ELSE 99 END::NUMBER``` |
| dst_endpoint.ip | ```DST_IP_ADDRESS::VARCHAR``` |
| dst_endpoint.port | ```DST_PORT_NUMBER::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'sentinelone-raw-events-v2'``` |
| metadata.product.vendor_name | ```'sentinelone'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```SRC_IP_ADDRESS::VARCHAR``` |
| src_endpoint.port | ```SRC_PORT_NUMBER::VARCHAR``` |
| status | ```CASE (CASE WHEN RAW:"event.network.connectionStatus"::VARCHAR IS NULL THEN 0 WHEN RAW:"event.network.connectionStatus"::VARCHAR = 'SUCCESS' THEN 1 WHEN RAW:"event.network.connectionStatus"::VARCHAR = 'FAILURE' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN RAW:"event.network.connectionStatus"::VARCHAR IS NULL THEN 0 WHEN RAW:"event.network.connectionStatus"::VARCHAR = 'SUCCESS' THEN 1 WHEN RAW:"event.network.connectionStatus"::VARCHAR = 'FAILURE' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (400199::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```400199::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
