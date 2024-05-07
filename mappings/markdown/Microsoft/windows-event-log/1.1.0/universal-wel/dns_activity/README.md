# Event Dossier: Universal Wel to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `windows-event-log`
* Product name: `universal-wel`
* Event codes: `PROVIDER ilike '%Microsoft-Windows-Dns-Client%' AND EVENT_ID IN (3006, 3016, 3009, 3010, 3019, 3012, 3013, 3008, 3018, 3020, 3011, 3014, 3007)`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN RAW:Message IS NULL THEN 0 WHEN RAW:Message ILIKE '%response%' THEN 2 WHEN RAW:Message ILIKE '%query%' AND RAW:Message NOT ILIKE '%response%' THEN 1 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN RAW:Message IS NULL THEN 0 WHEN RAW:Message ILIKE '%response%' THEN 2 WHEN RAW:Message ILIKE '%query%' AND RAW:Message NOT ILIKE '%response%' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.pid | ```RAW:ExecutionProcessID::NUMBER``` |
| actor.process.tid | ```RAW:ExecutionThreadID::NUMBER``` |
| actor.user.account.name | ```RAW:AccountName::VARCHAR``` |
| actor.user.uid | ```RAW:UserID::VARCHAR``` |
| answers | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT('rdata', REGEXP_SUBSTR(RAW:QueryResults, '[a-zA-Z0-9-]+(\\.[a-zA-Z0-9-]+){1,}|\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}\\.\\d{1,3}')))::VARIANT``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| device.domain | ```RAW:Domain::VARCHAR``` |
| device.hostname | ```MACHINE_NAME::VARCHAR``` |
| disposition | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```99::NUMBER``` |
| dst_endpoint.ip | ```MESSAGE_DETAILS:dns_server_ip::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', RAW:EventReceivedTime::TIMESTAMP_LTZ)``` |
| end_time_dt | ```RAW:EventReceivedTime::TIMESTAMP_LTZ``` |
| message | ```RAW:Message::VARCHAR``` |
| metadata.event_code | ```event_id``` |
| metadata.product.name | ```'universal-wel'``` |
| metadata.product.vendor_name | ```'windows-event-log'``` |
| metadata.version | ```'1.1.0'``` |
| query.hostname | ```MESSAGE_DETAILS:queried_domain::VARCHAR``` |
| query.opcode | ```RAW:Opcode::VARCHAR``` |
| query.opcode_id | ```RAW:OpcodeValue::NUMBER``` |
| query.type | ```MESSAGE_DETAILS:type::VARCHAR``` |
| rcode | ```CASE (CASE WHEN RAW:ResponseStatus::NUMBER BETWEEN 0 AND 11 THEN RAW:ResponseStatus::NUMBER WHEN RAW:ResponseStatus::NUMBER BETWEEN 16 AND 23 THEN RAW:ResponseStatus::NUMBER WHEN RAW:ResponseStatus::NUMBER BETWEEN 12 AND 15 THEN 24 WHEN RAW:ResponseStatus::NUMBER BETWEEN 24 AND 3840 THEN 24 WHEN RAW:ResponseStatus::NUMBER BETWEEN 4096 AND 65534 THEN 24 WHEN RAW:ResponseStatus::NUMBER BETWEEN 3841 AND 4095 THEN 25 WHEN RAW:ResponseStatus::NUMBER = 65535 THEN 25 ELSE 99 END::NUMBER) WHEN 0 THEN 'NoError' WHEN 1 THEN 'FormError' WHEN 10 THEN 'NotZone' WHEN 11 THEN 'DSOTYPENI' WHEN 16 THEN 'BADSIG_VERS' WHEN 17 THEN 'BADKEY' WHEN 18 THEN 'BADTIME' WHEN 19 THEN 'BADMODE' WHEN 2 THEN 'ServError' WHEN 20 THEN 'BADNAME' WHEN 21 THEN 'BADALG' WHEN 22 THEN 'BADTRUNC' WHEN 23 THEN 'BADCOOKIE' WHEN 24 THEN 'Unassigned' WHEN 25 THEN 'Reserved' WHEN 3 THEN 'NXDomain' WHEN 4 THEN 'NotImp' WHEN 5 THEN 'Refused' WHEN 6 THEN 'YXDomain' WHEN 7 THEN 'YXRRSet' WHEN 8 THEN 'NXRRSet' WHEN 9 THEN 'NotAuth' WHEN 99 THEN 'Other' END``` |
| rcode_id | ```CASE WHEN RAW:ResponseStatus::NUMBER BETWEEN 0 AND 11 THEN RAW:ResponseStatus::NUMBER WHEN RAW:ResponseStatus::NUMBER BETWEEN 16 AND 23 THEN RAW:ResponseStatus::NUMBER WHEN RAW:ResponseStatus::NUMBER BETWEEN 12 AND 15 THEN 24 WHEN RAW:ResponseStatus::NUMBER BETWEEN 24 AND 3840 THEN 24 WHEN RAW:ResponseStatus::NUMBER BETWEEN 4096 AND 65534 THEN 24 WHEN RAW:ResponseStatus::NUMBER BETWEEN 3841 AND 4095 THEN 25 WHEN RAW:ResponseStatus::NUMBER = 65535 THEN 25 ELSE 99 END::NUMBER``` |
| severity | ```CASE (CASE WHEN RAW:Severity IS NULL THEN 0 WHEN RAW:Severity = 'INFO' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN RAW:Severity IS NULL THEN 0 WHEN RAW:Severity = 'INFO' THEN 1 ELSE 99 END::NUMBER``` |
| src_endpoint.interface_name | ```RAW:AdapterName::VARCHAR``` |
| src_endpoint.interface_uid | ```RAW:InterfaceIndex::VARCHAR``` |
| src_endpoint.ip | ```MESSAGE_DETAILS:local_addresses[0]::VARCHAR``` |
| status_code | ```RAW:QueryStatus::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((400300 + (CASE WHEN RAW:Message IS NULL THEN 0 WHEN RAW:Message ILIKE '%response%' THEN 2 WHEN RAW:Message ILIKE '%query%' AND RAW:Message NOT ILIKE '%response%' THEN 1 ELSE 99 END))::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```(400300 + (CASE WHEN RAW:Message IS NULL THEN 0 WHEN RAW:Message ILIKE '%response%' THEN 2 WHEN RAW:Message ILIKE '%query%' AND RAW:Message NOT ILIKE '%response%' THEN 1 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
