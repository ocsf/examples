# Event Dossier: Pan Edr Raw Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `paloalto`
* Product name: `pan-edr-raw-logs`
* Event codes: `EVENT_TYPE = 2`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN event_sub_type IN (1, 2, 3, 7, 8, 9, 13) THEN 1 WHEN event_sub_type IN (4, 10, 11) THEN 2 WHEN event_sub_type = 6 THEN 4 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN event_sub_type IN (1, 2, 3, 7, 8, 9, 13) THEN 1 WHEN event_sub_type IN (4, 10, 11) THEN 2 WHEN event_sub_type = 6 THEN 4 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```OS_ACTOR_PROCESS_COMMAND_LINE::VARCHAR``` |
| actor.process.file.hashes | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('algorithm', CASE (case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 0 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 99 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'MD5' WHEN 2 THEN 'SHA-1' WHEN 3 THEN 'SHA-256' WHEN 4 THEN 'SHA-512' WHEN 5 THEN 'CTPH' WHEN 6 THEN 'TLSH' WHEN 7 THEN 'quickXorHash' WHEN 99 THEN 'Other' END, 'algorithm_id', case when OS_ACTOR_PROCESS_IMAGE_SHA256 is null and OS_ACTOR_PROCESS_IMAGE_MD5 is null then 0 when OS_ACTOR_PROCESS_IMAGE_SHA256 is not null then 3 when OS_ACTOR_PROCESS_IMAGE_MD5 is not null then 1 else 99 end::NUMBER, 'value', COALESCE(OS_ACTOR_PROCESS_IMAGE_SHA256, OS_ACTOR_PROCESS_IMAGE_MD5)::VARCHAR))``` |
| actor.process.file.name | ```OS_ACTOR_PROCESS_IMAGE_NAME::VARCHAR``` |
| actor.process.file.path | ```OS_ACTOR_PROCESS_IMAGE_PATH::VARCHAR``` |
| actor.process.pid | ```OS_ACTOR_PROCESS_OS_PID::NUMBER``` |
| actor.process.tid | ```OS_ACTOR_THREAD_THREAD_ID::NUMBER``` |
| actor.user.name | ```OS_ACTOR_PRIMARY_USERNAME::VARCHAR``` |
| actor.user.uid | ```OS_ACTOR_PRIMARY_USER_SID::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```CASE WHEN ACTION_NETWORK_PROTOCOL=6 THEN 'tcp' WHEN ACTION_NETWORK_PROTOCOL=17 THEN 'udp' ELSE NULL END::VARCHAR``` |
| connection_info.protocol_num | ```ACTION_NETWORK_PROTOCOL::NUMBER``` |
| connection_info.session.created_time | ```date_part('epoch_milliseconds', ACTION_NETWORK_CREATION_TIME::TIMESTAMP_LTZ)``` |
| connection_info.session.created_time_dt | ```ACTION_NETWORK_CREATION_TIME::TIMESTAMP_LTZ``` |
| connection_info.uid | ```ACTION_NETWORK_CONNECTION_ID::VARCHAR``` |
| device.hostname | ```AGENT_HOSTNAME::VARCHAR``` |
| device.ip | ```COALESCE(AGENT_IP_ADDRESSES[0], AGENT_IP_ADDRESSES_V6[0])::VARCHAR``` |
| device.mac | ```AGENT_INTERFACE_MAP_MAC[0]::VARCHAR``` |
| device.os.type | ```CASE (case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```case when AGENT_OS_TYPE = 1 then 100 when AGENT_OS_TYPE = 2 then 300 when AGENT_OS_TYPE = 4 then 200 else 0 end::NUMBER``` |
| device.os.version | ```AGENT_OS_SUB_TYPE::VARCHAR``` |
| device.uid | ```AGENT_ID::VARCHAR``` |
| dst_endpoint.ip | ```ACTION_REMOTE_IP::VARCHAR``` |
| dst_endpoint.port | ```ACTION_REMOTE_PORT::VARCHAR``` |
| metadata.product.name | ```'pan-edr-raw-logs'``` |
| metadata.product.vendor_name | ```'paloalto'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```ACTION_LOCAL_IP::VARCHAR``` |
| src_endpoint.port | ```ACTION_LOCAL_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```event_timestamp::TIMESTAMP_LTZ``` |
| traffic.bytes | ```(ACTION_TOTAL_UPLOAD + ACTION_TOTAL_DOWNLOAD)::NUMBER``` |
| traffic.bytes_in | ```ACTION_TOTAL_DOWNLOAD::NUMBER``` |
| traffic.bytes_out | ```ACTION_TOTAL_UPLOAD::NUMBER``` |
| type_name | ```CASE ((400100 + CASE WHEN event_sub_type IN (1, 2, 3, 7, 8, 9, 13) THEN 1 WHEN event_sub_type IN (4, 10, 11) THEN 2 WHEN event_sub_type = 6 THEN 4 ELSE 99 END)::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```(400100 + CASE WHEN event_sub_type IN (1, 2, 3, 7, 8, 9, 13) THEN 1 WHEN event_sub_type IN (4, 10, 11) THEN 2 WHEN event_sub_type = 6 THEN 4 ELSE 99 END)::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
