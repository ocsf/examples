# Event Dossier: Vectra Metadata Logs to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `vectra`
* Product name: `vectra-metadata-logs`
* Event codes: `METADATA_TYPE = 'metadata_dns'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN RAW:rejected = 'false' THEN 1 WHEN RAW:rejected = 'true' THEN 2 WHEN RAW:rejected IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN RAW:rejected = 'false' THEN 1 WHEN RAW:rejected = 'true' THEN 2 WHEN RAW:rejected IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.session.is_remote | ```LOCAL_RESP::BOOLEAN``` |
| actor.session.uid | ```ORIG_SLUID::VARCHAR``` |
| answers | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT('rdata', RAW:answers, 'ttl', TTLS))::ARRAY``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_name | ```CASE WHEN PROTO = 6 THEN 'tcp' WHEN PROTO = 17 THEN 'udp' END::VARCHAR``` |
| connection_info.protocol_num | ```PROTO::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(ID_ORIG_H, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(ID_ORIG_H, 'INET'):family::NUMBER``` |
| connection_info.session.is_remote | ```LOCAL_ORIG::BOOLEAN``` |
| connection_info.session.uid | ```RESP_SLUID::VARCHAR``` |
| connection_info.uid | ```UID::VARCHAR``` |
| disposition | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```0::NUMBER``` |
| dst_endpoint.hostname | ```RESP_HOSTNAME::VARCHAR``` |
| dst_endpoint.ip | ```ID_RESP_H::VARCHAR``` |
| dst_endpoint.port | ```RAW['id.resp_p']::VARCHAR``` |
| dst_endpoint.uid | ```RESP_HUID::VARCHAR``` |
| load_balancer.uid | ```SENSOR_UID::VARCHAR``` |
| metadata.event_code | ```METADATA_TYPE``` |
| metadata.product.name | ```'vectra-metadata-logs'``` |
| metadata.product.vendor_name | ```'vectra'``` |
| metadata.version | ```'1.1.0'``` |
| query.class | ```RAW:qclass_name::VARCHAR``` |
| query.hostname | ```QUERY::VARCHAR``` |
| query.type | ```QTYPE_NAME::VARCHAR``` |
| rcode | ```CASE (CASE WHEN RAW:rcode_name = 'NoError' THEN 0 WHEN RAW:rcode_name = 'FormErr' THEN 1 WHEN RAW:rcode_name = 'ServFail' THEN 2 WHEN RAW:rcode_name = 'NXDomain' THEN 3 WHEN RAW:rcode_name = 'NotImp' THEN 4 WHEN RAW:rcode_name = 'Refused' THEN 5 WHEN RAW:rcode_name = 'YXRRSet' THEN 7 WHEN RAW:rcode_name = 'NotAuth' THEN 9 WHEN RAW:rcode_name IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'NoError' WHEN 1 THEN 'FormError' WHEN 10 THEN 'NotZone' WHEN 11 THEN 'DSOTYPENI' WHEN 16 THEN 'BADSIG_VERS' WHEN 17 THEN 'BADKEY' WHEN 18 THEN 'BADTIME' WHEN 19 THEN 'BADMODE' WHEN 2 THEN 'ServError' WHEN 20 THEN 'BADNAME' WHEN 21 THEN 'BADALG' WHEN 22 THEN 'BADTRUNC' WHEN 23 THEN 'BADCOOKIE' WHEN 24 THEN 'Unassigned' WHEN 25 THEN 'Reserved' WHEN 3 THEN 'NXDomain' WHEN 4 THEN 'NotImp' WHEN 5 THEN 'Refused' WHEN 6 THEN 'YXDomain' WHEN 7 THEN 'YXRRSet' WHEN 8 THEN 'NXRRSet' WHEN 9 THEN 'NotAuth' WHEN 99 THEN 'Other' END``` |
| rcode_id | ```CASE WHEN RAW:rcode_name = 'NoError' THEN 0 WHEN RAW:rcode_name = 'FormErr' THEN 1 WHEN RAW:rcode_name = 'ServFail' THEN 2 WHEN RAW:rcode_name = 'NXDomain' THEN 3 WHEN RAW:rcode_name = 'NotImp' THEN 4 WHEN RAW:rcode_name = 'Refused' THEN 5 WHEN RAW:rcode_name = 'YXRRSet' THEN 7 WHEN RAW:rcode_name = 'NotAuth' THEN 9 WHEN RAW:rcode_name IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.hostname | ```RAW:orig_hostname::VARCHAR``` |
| src_endpoint.ip | ```ID_ORIG_H::VARCHAR``` |
| src_endpoint.port | ```ID_ORIG_P::VARCHAR``` |
| src_endpoint.uid | ```ORIG_HUID::VARCHAR``` |
| status | ```CASE (CASE WHEN RAW:rejected = 'false' THEN 1 WHEN RAW:rejected = 'true' THEN 2 WHEN RAW:rejected IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN RAW:rejected = 'false' THEN 1 WHEN RAW:rejected = 'true' THEN 2 WHEN RAW:rejected IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (400301::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```400301::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
