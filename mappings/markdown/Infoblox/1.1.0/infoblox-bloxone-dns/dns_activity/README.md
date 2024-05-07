# Event Dossier: Infoblox Bloxone Dns to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `infoblox`
* Product name: `infoblox-bloxone-dns`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```CASE WHEN OPCODE IS NULL THEN 0 WHEN OPCODE = 'Query' THEN 1 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN OPCODE IS NULL THEN 0 WHEN OPCODE = 'Query' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| answers | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT('flag_ids', ARRAY_CONSTRUCT( CASE WHEN RESPONDER_FLAGS:responder_authoritative_answer::BOOLEAN = TRUE THEN 1 ELSE 99 END, CASE WHEN RESPONDER_FLAGS:responder_truncated::BOOLEAN = TRUE THEN 2 ELSE 99 END, CASE WHEN RESPONDER_FLAGS:responder_recursion_desired::BOOLEAN = TRUE THEN 3 ELSE 99 END, CASE WHEN RESPONDER_FLAGS:responder_recursion_available::BOOLEAN = TRUE THEN 4 ELSE 99 END, CASE WHEN RESPONDER_FLAGS:responder_authentic_data::BOOLEAN = TRUE THEN 5 ELSE 99 END, CASE WHEN RESPONDER_FLAGS:responder_checking_disabled::BOOLEAN = TRUE THEN 6 ELSE 99 END)::ARRAY))::ARRAY``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| cloud.region | ```REGION::VARCHAR``` |
| connection_info.protocol_name | ```CASE WHEN PROTOCOL = 6 THEN 'tcp' WHEN PROTOCOL = 17 THEN 'udp' ELSE NULL END::VARCHAR``` |
| connection_info.protocol_num | ```PROTOCOL::NUMBER``` |
| device.org.uid | ```CLIENT_IDENTIFIER::VARCHAR``` |
| disposition | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```99::NUMBER``` |
| dst_endpoint.ip | ```RESPONDER_IP::VARCHAR``` |
| dst_endpoint.port | ```RESPONDER_PORT::VARCHAR``` |
| metadata.product.name | ```'infoblox-bloxone-dns'``` |
| metadata.product.vendor_name | ```'infoblox'``` |
| metadata.version | ```'1.1.0'``` |
| query.class | ```RAW:qclass::VARCHAR``` |
| query.hostname | ```QUERY_NAME::VARCHAR``` |
| query.type | ```RESOURCE_RECORD_TYPE::VARCHAR``` |
| rcode | ```CASE (CASE WHEN RETURN_CODE = 'NoError' THEN 0 WHEN RETURN_CODE = 'FORMERR' THEN 1 WHEN RETURN_CODE = 'ServFail' THEN 2 WHEN RETURN_CODE = 'NXDomain' THEN 3 WHEN RETURN_CODE = 'REFUSED' THEN 5 WHEN RETURN_CODE = 'ServFail' THEN 2 WHEN RETURN_CODE = 'NXDomain' THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'NoError' WHEN 1 THEN 'FormError' WHEN 10 THEN 'NotZone' WHEN 11 THEN 'DSOTYPENI' WHEN 16 THEN 'BADSIG_VERS' WHEN 17 THEN 'BADKEY' WHEN 18 THEN 'BADTIME' WHEN 19 THEN 'BADMODE' WHEN 2 THEN 'ServError' WHEN 20 THEN 'BADNAME' WHEN 21 THEN 'BADALG' WHEN 22 THEN 'BADTRUNC' WHEN 23 THEN 'BADCOOKIE' WHEN 24 THEN 'Unassigned' WHEN 25 THEN 'Reserved' WHEN 3 THEN 'NXDomain' WHEN 4 THEN 'NotImp' WHEN 5 THEN 'Refused' WHEN 6 THEN 'YXDomain' WHEN 7 THEN 'YXRRSet' WHEN 8 THEN 'NXRRSet' WHEN 9 THEN 'NotAuth' WHEN 99 THEN 'Other' END``` |
| rcode_id | ```CASE WHEN RETURN_CODE = 'NoError' THEN 0 WHEN RETURN_CODE = 'FORMERR' THEN 1 WHEN RETURN_CODE = 'ServFail' THEN 2 WHEN RETURN_CODE = 'NXDomain' THEN 3 WHEN RETURN_CODE = 'REFUSED' THEN 5 WHEN RETURN_CODE = 'ServFail' THEN 2 WHEN RETURN_CODE = 'NXDomain' THEN 3 ELSE 99 END::NUMBER``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```REQUESTER_IP::VARCHAR``` |
| src_endpoint.port | ```REQUESTER_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((400300 + (CASE WHEN OPCODE IS NULL THEN 0 WHEN OPCODE = 'Query' THEN 1 ELSE 99 END))::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```(400300 + (CASE WHEN OPCODE IS NULL THEN 0 WHEN OPCODE = 'Query' THEN 1 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
