# Event Dossier: Cloudflare Dns to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `cloudflare`
* Product name: `cloudflare-dns`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| metadata.product.name | ```'cloudflare-dns'``` |
| metadata.product.vendor_name | ```'cloudflare'``` |
| metadata.version | ```'1.1.0'``` |
| query.hostname | ```QUERY_NAME::VARCHAR``` |
| query.type | ```QUERY_TYPE::VARCHAR``` |
| rcode | ```CASE (CASE WHEN RESPONSE_CODE BETWEEN 0 AND 11 THEN RESPONSE_CODE WHEN RESPONSE_CODE BETWEEN 16 AND 23 THEN RESPONSE_CODE WHEN RESPONSE_CODE BETWEEN 12 AND 15 THEN 24 WHEN RESPONSE_CODE BETWEEN 24 AND 3840 THEN 24 WHEN RESPONSE_CODE BETWEEN 4096 AND 65534 THEN 24 WHEN RESPONSE_CODE BETWEEN 3841 AND 4095 THEN 25 WHEN RESPONSE_CODE = 65535 THEN 25 ELSE 99 END::NUMBER) WHEN 0 THEN 'NoError' WHEN 1 THEN 'FormError' WHEN 10 THEN 'NotZone' WHEN 11 THEN 'DSOTYPENI' WHEN 16 THEN 'BADSIG_VERS' WHEN 17 THEN 'BADKEY' WHEN 18 THEN 'BADTIME' WHEN 19 THEN 'BADMODE' WHEN 2 THEN 'ServError' WHEN 20 THEN 'BADNAME' WHEN 21 THEN 'BADALG' WHEN 22 THEN 'BADTRUNC' WHEN 23 THEN 'BADCOOKIE' WHEN 24 THEN 'Unassigned' WHEN 25 THEN 'Reserved' WHEN 3 THEN 'NXDomain' WHEN 4 THEN 'NotImp' WHEN 5 THEN 'Refused' WHEN 6 THEN 'YXDomain' WHEN 7 THEN 'YXRRSet' WHEN 8 THEN 'NXRRSet' WHEN 9 THEN 'NotAuth' WHEN 99 THEN 'Other' END``` |
| rcode_id | ```CASE WHEN RESPONSE_CODE BETWEEN 0 AND 11 THEN RESPONSE_CODE WHEN RESPONSE_CODE BETWEEN 16 AND 23 THEN RESPONSE_CODE WHEN RESPONSE_CODE BETWEEN 12 AND 15 THEN 24 WHEN RESPONSE_CODE BETWEEN 24 AND 3840 THEN 24 WHEN RESPONSE_CODE BETWEEN 4096 AND 65534 THEN 24 WHEN RESPONSE_CODE BETWEEN 3841 AND 4095 THEN 25 WHEN RESPONSE_CODE = 65535 THEN 25 ELSE 99 END::NUMBER``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (400399::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```400399::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
