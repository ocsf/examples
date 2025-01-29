# Event Dossier: Universal Wel to OCSF class Win/registry Key Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_key_activity`
* Vendor name: `windows-event-log`
* Product name: `universal-wel`
* Event codes: `raw:Category = 'Registry' AND EVENT_ID = 4663`
---

| OCSF | RAW |
| --- | --- |
| access_mask | ```TO_NUMBER(SUBSTRING(RAW:AccessMask, 3), 'XX')::NUMBER``` |
| action | ```CASE (CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = TRUE THEN 1 WHEN AUDIT_SUCCESS = FALSE THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = TRUE THEN 1 WHEN AUDIT_SUCCESS = FALSE THEN 2 ELSE 99 END::NUMBER``` |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Create' WHEN 2 THEN 'Read' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 5 THEN 'Rename' WHEN 6 THEN 'Set Security' WHEN 7 THEN 'Restore' WHEN 8 THEN 'Import' WHEN 9 THEN 'Export' WHEN 99 THEN 'Other' END``` |
| actor.process.file.name | ```MESSAGE_DETAILS:process_information:process_name::VARCHAR``` |
| actor.process.pid | ```RAW:ExecutionProcessID::NUMBER``` |
| actor.process.tid | ```RAW:ExecutionThreadID::NUMBER``` |
| actor.process.uid | ```MESSAGE_DETAILS:process_information:process_id::VARCHAR``` |
| actor.user.account.name | ```MESSAGE_DETAILS:subject:account_name::VARCHAR``` |
| actor.user.domain | ```MESSAGE_DETAILS:subject:account_domain::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'win/registry_key_activity'``` |
| class_uid | ```201001``` |
| device.hostname | ```MACHINE_NAME::VARCHAR``` |
| device.ip | ```RAW:MessageSourceAddress::VARCHAR``` |
| disposition | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```99::NUMBER``` |
| end_time | ```date_part('epoch_milliseconds', to_varchar(RAW:EventReceivedTime::TIMESTAMP_LTZ, 'YYYY-MM-DD"T"HH24:MI:SS.FF3"Z"')::TIMESTAMP_LTZ)``` |
| end_time_dt | ```to_varchar(RAW:EventReceivedTime::TIMESTAMP_LTZ, 'YYYY-MM-DD"T"HH24:MI:SS.FF3"Z"')``` |
| message | ```RAW:Message::VARCHAR``` |
| metadata.event_code | ```event_id``` |
| metadata.product.name | ```'universal-wel'``` |
| metadata.product.vendor_name | ```'windows-event-log'``` |
| metadata.version | ```'1.1.0'``` |
| reg_key.path | ```MESSAGE_DETAILS:object:object_name::VARCHAR``` |
| severity | ```CASE (CASE WHEN RAW:Severity IS NULL THEN 0 WHEN RAW:Severity = 'INFO' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN RAW:Severity IS NULL THEN 0 WHEN RAW:Severity = 'INFO' THEN 1 ELSE 99 END::NUMBER``` |
| status | ```CASE (CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = TRUE THEN 1 WHEN AUDIT_SUCCESS = FALSE THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = TRUE THEN 1 WHEN AUDIT_SUCCESS = FALSE THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (20100199::NUMBER) WHEN 20100100 THEN 'Registry Key Activity: Unknown' WHEN 20100101 THEN 'Registry Key Activity: Create' WHEN 20100102 THEN 'Registry Key Activity: Read' WHEN 20100103 THEN 'Registry Key Activity: Modify' WHEN 20100104 THEN 'Registry Key Activity: Delete' WHEN 20100105 THEN 'Registry Key Activity: Rename' WHEN 20100106 THEN 'Registry Key Activity: Set Security' WHEN 20100107 THEN 'Registry Key Activity: Restore' WHEN 20100108 THEN 'Registry Key Activity: Import' WHEN 20100109 THEN 'Registry Key Activity: Export' WHEN 20100199 THEN 'Registry Key Activity: Other' END``` |
| type_uid | ```20100199::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
