# Event Dossier: Osquery Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `osquery`
* Product name: `osquery-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```(CASE WHEN EVENT_TYPE IS NULL THEN 0 ELSE 99 END)::NUMBER``` |
| activity_name | ```CASE ((CASE WHEN EVENT_TYPE IS NULL THEN 0 ELSE 99 END)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ``` COMMAND_LINE::VARCHAR``` |
| actor.process.file.name | ```COLUMNS:name::VARCHAR``` |
| actor.process.file.path | ```PATH::VARCHAR``` |
| actor.process.parent_process.file.name | ```COLUMNS:parentname::VARCHAR``` |
| actor.process.parent_process.file.path | ```COLUMNS:parentpath::VARCHAR``` |
| actor.process.parent_process.pid | ```COLUMNS:parentid::NUMBER``` |
| actor.process.pid | ```COLUMNS:pid::NUMBER``` |
| actor.process.user.name | ```COALESCE(USER, COLUMNS:username)::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```CASE WHEN IFF(LEN(COLUMNS:protocol)>=1,COLUMNS:protocol,NULL)::NUMBER = 0 THEN 'HOPOPT' WHEN IFF(LEN(COLUMNS:protocol)>=1,COLUMNS:protocol,NULL)::NUMBER = 17 THEN 'UDP' WHEN IFF(LEN(COLUMNS:protocol)>=1,COLUMNS:protocol,NULL)::NUMBER = 3 THEN 'GGP' WHEN IFF(LEN(COLUMNS:protocol)>=1,COLUMNS:protocol,NULL)::NUMBER = 2 THEN 'IGMP' WHEN IFF(LEN(COLUMNS:protocol)>=1,COLUMNS:protocol,NULL)::NUMBER = 1 THEN 'ICMP' WHEN IFF(LEN(COLUMNS:protocol)>=1,COLUMNS:protocol,NULL)::NUMBER = 6 THEN 'TCP' ELSE NULL::VARCHAR END``` |
| connection_info.protocol_num | ```IFF(LEN(COLUMNS:protocol)>=1,COLUMNS:protocol,NULL)::NUMBER``` |
| count | ```COUNTER::NUMBER``` |
| device.hostname | ```COALESCE(HOST, HOST_IDENTIFIER)::VARCHAR``` |
| dst_endpoint.ip | ```COLUMNS:remote_address::VARCHAR``` |
| dst_endpoint.port | ```COLUMNS:remote_port::VARCHAR``` |
| metadata.product.name | ```'osquery-logs'``` |
| metadata.product.vendor_name | ```'osquery'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```COLUMNS:local_address::VARCHAR``` |
| src_endpoint.port | ```COLUMNS:local_port::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((4001*100 + (CASE WHEN EVENT_TYPE IS NULL THEN 0 ELSE 99 END)::NUMBER)::NUMBER) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```(4001*100 + (CASE WHEN EVENT_TYPE IS NULL THEN 0 ELSE 99 END)::NUMBER)::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
