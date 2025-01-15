# Event Dossier: Universal Wel to OCSF class Win/registry Value Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `registry_value_activity`
* Vendor name: `windows-event-log`
* Product name: `universal-wel`
* Event codes: `RAW:Category = 'Registry' AND EVENT_ID = 4657`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = true THEN 1 WHEN AUDIT_SUCCESS = false THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = true THEN 1 WHEN AUDIT_SUCCESS = false THEN 2 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN MESSAGE_DETAILS:object:operation_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:object:operation_type ILIKE '%modified%' THEN 3 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN MESSAGE_DETAILS:object:operation_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:object:operation_type ILIKE '%modified%' THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Get' WHEN 2 THEN 'Set' WHEN 3 THEN 'Modify' WHEN 4 THEN 'Delete' WHEN 99 THEN 'Other' END``` |
| actor.process.file.path | ```MESSAGE_DETAILS:process_information:process_name::VARCHAR``` |
| actor.process.pid | ```RAW:ExecutionProcessID::NUMBER``` |
| actor.process.tid | ```RAW:ExecutionThreadID::NUMBER``` |
| actor.process.uid | ```MESSAGE_DETAILS:process_information:process_id::VARCHAR``` |
| actor.user.account.name | ```MESSAGE_DETAILS:subject:account_name::VARCHAR``` |
| actor.user.domain | ```MESSAGE_DETAILS:subject:account_domain::VARCHAR``` |
| category_name | ```CASE (1::NUMBER) WHEN 1 THEN 'System Activity' END``` |
| category_uid | ```1::NUMBER``` |
| class_name | ```'win/registry_value_activity'``` |
| class_uid | ```201002``` |
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
| prev_reg_value.type | ```CASE (CASE WHEN MESSAGE_DETAILS:change_information:old_value_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:change_information:old_value_type = 'REG_SZ' THEN 10 WHEN MESSAGE_DETAILS:change_information:old_value_type = 'REG_DWORD' THEN 2 WHEN MESSAGE_DETAILS:change_information:old_value_type = 'REG_BINARY' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'REG_BINARY' WHEN 10 THEN 'REG_SZ' WHEN 2 THEN 'REG_DWORD' WHEN 3 THEN 'REG_DWORD_BIG_ENDIAN' WHEN 4 THEN 'REG_EXPAND_SZ' WHEN 5 THEN 'REG_LINK' WHEN 6 THEN 'REG_MULTI_SZ' WHEN 7 THEN 'REG_NONE' WHEN 8 THEN 'REG_QWORD' WHEN 9 THEN 'REG_QWORD_LITTLE_ENDIAN' WHEN 99 THEN 'Other' END``` |
| prev_reg_value.type_id | ```CASE WHEN MESSAGE_DETAILS:change_information:old_value_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:change_information:old_value_type = 'REG_SZ' THEN 10 WHEN MESSAGE_DETAILS:change_information:old_value_type = 'REG_DWORD' THEN 2 WHEN MESSAGE_DETAILS:change_information:old_value_type = 'REG_BINARY' THEN 1 ELSE 99 END::NUMBER``` |
| reg_value.name | ```MESSAGE_DETAILS:object:object_value_name::VARCHAR``` |
| reg_value.path | ```MESSAGE_DETAILS:object:object_name::VARCHAR``` |
| reg_value.type | ```CASE (CASE WHEN MESSAGE_DETAILS:change_information:new_value_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:change_information:new_value_type = 'REG_SZ' THEN 10 WHEN MESSAGE_DETAILS:change_information:new_value_type = 'REG_DWORD' THEN 2 WHEN MESSAGE_DETAILS:change_information:new_value_type = 'REG_BINARY' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'REG_BINARY' WHEN 10 THEN 'REG_SZ' WHEN 2 THEN 'REG_DWORD' WHEN 3 THEN 'REG_DWORD_BIG_ENDIAN' WHEN 4 THEN 'REG_EXPAND_SZ' WHEN 5 THEN 'REG_LINK' WHEN 6 THEN 'REG_MULTI_SZ' WHEN 7 THEN 'REG_NONE' WHEN 8 THEN 'REG_QWORD' WHEN 9 THEN 'REG_QWORD_LITTLE_ENDIAN' WHEN 99 THEN 'Other' END``` |
| reg_value.type_id | ```CASE WHEN MESSAGE_DETAILS:change_information:new_value_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:change_information:new_value_type = 'REG_SZ' THEN 10 WHEN MESSAGE_DETAILS:change_information:new_value_type = 'REG_DWORD' THEN 2 WHEN MESSAGE_DETAILS:change_information:new_value_type = 'REG_BINARY' THEN 1 ELSE 99 END::NUMBER``` |
| severity | ```CASE (CASE WHEN RAW:Severity IS NULL THEN 0 WHEN RAW:Severity = 'INFO' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN RAW:Severity IS NULL THEN 0 WHEN RAW:Severity = 'INFO' THEN 1 ELSE 99 END::NUMBER``` |
| status | ```CASE (CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = true THEN 1 WHEN AUDIT_SUCCESS = false THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN AUDIT_SUCCESS IS NULL THEN 0 WHEN AUDIT_SUCCESS = true THEN 1 WHEN AUDIT_SUCCESS = false THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((20100200 + (CASE WHEN MESSAGE_DETAILS:object:operation_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:object:operation_type ILIKE '%modified%' THEN 3 ELSE 99 END))::NUMBER) WHEN 20100200 THEN 'Registry Value Activity: Unknown' WHEN 20100201 THEN 'Registry Value Activity: Get' WHEN 20100202 THEN 'Registry Value Activity: Set' WHEN 20100203 THEN 'Registry Value Activity: Modify' WHEN 20100204 THEN 'Registry Value Activity: Delete' WHEN 20100299 THEN 'Registry Value Activity: Other' END``` |
| type_uid | ```(20100200 + (CASE WHEN MESSAGE_DETAILS:object:operation_type IS NULL THEN 0 WHEN MESSAGE_DETAILS:object:operation_type ILIKE '%modified%' THEN 3 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
