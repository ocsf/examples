# Event Dossier: Infoblox Nios Dns to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `infoblox`
* Product name: `infoblox-nios-dns`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'query' THEN 1 WHEN EVENT_TYPE = 'response' THEN 2 WHEN EVENT_TYPE = 'traffic' THEN 6 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'query' THEN 1 WHEN EVENT_TYPE = 'response' THEN 2 WHEN EVENT_TYPE = 'traffic' THEN 6 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| answers | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT('flag_ids', ARRAY_CONSTRUCT(CASE WHEN FLAGS IS NULL THEN 0 WHEN FLAGS = 'A' THEN 1 WHEN FLAGS = 'T' THEN 2 ELSE 99 END), 'class', RESPONSE_RECORDS[0].class, 'type', RESPONSE_RECORDS[0].type, 'ttl', RESPONSE_RECORDS[0].ttl))::ARRAY``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| connection_info.protocol_name | ```PROTOCOL::VARCHAR``` |
| disposition | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```99::NUMBER``` |
| dst_endpoint.ip | ```NAME_SERVER_IP::VARCHAR``` |
| metadata.product.name | ```'infoblox-nios-dns'``` |
| metadata.product.vendor_name | ```'infoblox'``` |
| metadata.version | ```'1.1.0'``` |
| query.class | ```CLASS::VARCHAR``` |
| query.hostname | ```QUERIED_DOMAIN::VARCHAR``` |
| query.type | ```TYPE::VARCHAR``` |
| rcode | ```CASE (CASE WHEN RESPONSE_CODE = 'NOERROR' THEN 0 WHEN RESPONSE_CODE = 'FORMERR' THEN 1 WHEN RESPONSE_CODE = 'SERVFAIL' THEN 2 WHEN RESPONSE_CODE = 'NXDOMAIN' THEN 3 WHEN RESPONSE_CODE = 'REFUSED' THEN 5 WHEN RESPONSE_CODE = 'NOTAUTH' THEN 9 WHEN RESPONSE_CODE = 'BADVERS' THEN 16 ELSE 99 END::NUMBER) WHEN 0 THEN 'NoError' WHEN 1 THEN 'FormError' WHEN 10 THEN 'NotZone' WHEN 11 THEN 'DSOTYPENI' WHEN 16 THEN 'BADSIG_VERS' WHEN 17 THEN 'BADKEY' WHEN 18 THEN 'BADTIME' WHEN 19 THEN 'BADMODE' WHEN 2 THEN 'ServError' WHEN 20 THEN 'BADNAME' WHEN 21 THEN 'BADALG' WHEN 22 THEN 'BADTRUNC' WHEN 23 THEN 'BADCOOKIE' WHEN 24 THEN 'Unassigned' WHEN 25 THEN 'Reserved' WHEN 3 THEN 'NXDomain' WHEN 4 THEN 'NotImp' WHEN 5 THEN 'Refused' WHEN 6 THEN 'YXDomain' WHEN 7 THEN 'YXRRSet' WHEN 8 THEN 'NXRRSet' WHEN 9 THEN 'NotAuth' WHEN 99 THEN 'Other' END``` |
| rcode_id | ```CASE WHEN RESPONSE_CODE = 'NOERROR' THEN 0 WHEN RESPONSE_CODE = 'FORMERR' THEN 1 WHEN RESPONSE_CODE = 'SERVFAIL' THEN 2 WHEN RESPONSE_CODE = 'NXDOMAIN' THEN 3 WHEN RESPONSE_CODE = 'REFUSED' THEN 5 WHEN RESPONSE_CODE = 'NOTAUTH' THEN 9 WHEN RESPONSE_CODE = 'BADVERS' THEN 16 ELSE 99 END::NUMBER``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```REQUESTER_IP::VARCHAR``` |
| src_endpoint.port | ```REQUESTER_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((400300 + (CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'query' THEN 1 WHEN EVENT_TYPE = 'response' THEN 2 WHEN EVENT_TYPE = 'traffic' THEN 6 ELSE 99 END))::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```(400300 + (CASE WHEN EVENT_TYPE IS NULL THEN 0 WHEN EVENT_TYPE = 'query' THEN 1 WHEN EVENT_TYPE = 'response' THEN 2 WHEN EVENT_TYPE = 'traffic' THEN 6 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
