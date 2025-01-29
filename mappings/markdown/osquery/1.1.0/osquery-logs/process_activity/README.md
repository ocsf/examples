# Event Dossier: Osquery Logs to OCSF class Process Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `process_activity`
* Vendor name: `osquery`
* Product name: `osquery-logs`
* Event codes: `EVENT_TYPE ILIKE ANY ('%process%', '%Process%')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN EVENT_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN EVENT_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Launch' WHEN 2 THEN 'Terminate' WHEN 3 THEN 'Open' WHEN 4 THEN 'Inject' WHEN 5 THEN 'Set User ID' WHEN 99 THEN 'Other' END``` |
| actor.process.cmd_line | ```COALESCE(COMMAND_LINE, COLUMNS:cmdline)::VARCHAR``` |
| actor.process.file.name | ```COLUMNS:name::VARCHAR``` |
| actor.process.file.path | ```COALESCE(COLUMNS:path, COLUMNS:child_path)::VARCHAR``` |
| actor.process.name | ```COLUMNS:child_process::VARCHAR``` |
| actor.process.parent_process.file.path | ```COLUMNS:parent_path::VARCHAR``` |
| actor.process.parent_process.name | ```COLUMNS:parent_process::VARCHAR``` |
| actor.process.parent_process.pid | ```COLUMNS:parent_pid::NUMBER``` |
| actor.process.pid | ```COALESCE(COLUMNS:pid, COLUMNS:child_pid)::NUMBER``` |
| actor.process.uid | ```COLUMNS:uid::VARCHAR``` |
| actor.process.user.name | ```COALESCE(USER, COLUMNS:username)::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'process_activity'``` |
| class_uid | ```1007``` |
| metadata.product.name | ```'osquery-logs'``` |
| metadata.product.vendor_name | ```'osquery'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN EVENT_TYPE IS NULL THEN 100700 ELSE 100799 END::NUMBER) WHEN 100700 THEN 'Process Activity: Unknown' WHEN 100701 THEN 'Process Activity: Launch' WHEN 100702 THEN 'Process Activity: Terminate' WHEN 100703 THEN 'Process Activity: Open' WHEN 100704 THEN 'Process Activity: Inject' WHEN 100705 THEN 'Process Activity: Set User ID' WHEN 100799 THEN 'Process Activity: Other' END``` |
| type_uid | ```CASE WHEN EVENT_TYPE IS NULL THEN 100700 ELSE 100799 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
