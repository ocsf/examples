# Event Dossier: Cisco Umbrella Dns Logs to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `cisco-umbrella`
* Product name: `cisco-umbrella-dns-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION IS NULL THEN 0 WHEN ACTION = 'Allowed' THEN 1 WHEN ACTION = 'Blocked' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION IS NULL THEN 0 WHEN ACTION = 'Allowed' THEN 1 WHEN ACTION = 'Blocked' THEN 2 ELSE 99 END::NUMBER``` |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| metadata.product.name | ```'cisco-umbrella-dns-logs'``` |
| metadata.product.vendor_name | ```'cisco-umbrella'``` |
| metadata.version | ```'1.1.0'``` |
| query.hostname | ```DOMAIN::VARCHAR``` |
| query.type | ```REGEXP_SUBSTR(QUERY_TYPE, '([A-Za-z]+)')::VARCHAR``` |
| rcode | ```CASE (CASE WHEN RESPONSE_CODE = 'NOERROR' THEN 0 WHEN RESPONSE_CODE = 'SERVFAIL' THEN 2 WHEN RESPONSE_CODE = 'NXDOMAIN' THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'NoError' WHEN 1 THEN 'FormError' WHEN 10 THEN 'NotZone' WHEN 11 THEN 'DSOTYPENI' WHEN 16 THEN 'BADSIG_VERS' WHEN 17 THEN 'BADKEY' WHEN 18 THEN 'BADTIME' WHEN 19 THEN 'BADMODE' WHEN 2 THEN 'ServError' WHEN 20 THEN 'BADNAME' WHEN 21 THEN 'BADALG' WHEN 22 THEN 'BADTRUNC' WHEN 23 THEN 'BADCOOKIE' WHEN 24 THEN 'Unassigned' WHEN 25 THEN 'Reserved' WHEN 3 THEN 'NXDomain' WHEN 4 THEN 'NotImp' WHEN 5 THEN 'Refused' WHEN 6 THEN 'YXDomain' WHEN 7 THEN 'YXRRSet' WHEN 8 THEN 'NXRRSet' WHEN 9 THEN 'NotAuth' WHEN 99 THEN 'Other' END``` |
| rcode_id | ```CASE WHEN RESPONSE_CODE = 'NOERROR' THEN 0 WHEN RESPONSE_CODE = 'SERVFAIL' THEN 2 WHEN RESPONSE_CODE = 'NXDOMAIN' THEN 3 ELSE 99 END::NUMBER``` |
| src_endpoint.domain | ```DOMAIN::VARCHAR``` |
| src_endpoint.ip | ```COALESCE(INTERNAL_IP, EXTERNAL_IP)::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (400301::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```400301::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
