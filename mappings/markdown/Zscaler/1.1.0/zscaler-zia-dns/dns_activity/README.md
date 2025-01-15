# Event Dossier: Zscaler Zia Dns to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `zscaler`
* Product name: `zscaler-zia-dns`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN REQUEST_ACTION IS NULL THEN 0 WHEN REQUEST_ACTION = 'Allow' THEN 1 WHEN REQUEST_ACTION = 'Block' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN REQUEST_ACTION IS NULL THEN 0 WHEN REQUEST_ACTION = 'Allow' THEN 1 WHEN REQUEST_ACTION = 'Block' THEN 2 ELSE 99 END::NUMBER``` |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```IFF(ILIKE(USER, '%@%.com'), USER, NULL)::VARCHAR``` |
| actor.user.name | ```DEVICE_OWNER::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| device.location.city | ```SPLIT_PART(LOCATION, '->', 1)::VARCHAR``` |
| device.name | ```DEVICE_HOSTNAME::VARCHAR``` |
| dst_endpoint.ip | ```SRV_DESTINATION_IP::VARCHAR``` |
| dst_endpoint.port | ```SRV_DESTINATION_PORT::VARCHAR``` |
| duration | ```DURATION_MS::NUMBER``` |
| metadata.product.name | ```'zscaler-zia-dns'``` |
| metadata.product.vendor_name | ```'zscaler'``` |
| metadata.version | ```'1.1.0'``` |
| query.hostname | ```DNS_REQUEST::VARCHAR``` |
| query.type | ```DNS_REQUEST_TYPE::VARCHAR``` |
| rcode | ```CASE (IFF(REGEXP_LIKE(DNS_RESPONSE, '[A-Za-z]+'), CASE WHEN DNS_RESPONSE = 'NOERROR' THEN 0 WHEN DNS_RESPONSE = 'FORMERR' THEN 1 WHEN DNS_RESPONSE = 'SERVFAIL' THEN 2 WHEN DNS_RESPONSE = 'NXDOMAIN' THEN 3 WHEN DNS_RESPONSE = 'NOTIMP' THEN 4 WHEN DNS_RESPONSE = 'REFUSED' THEN 5 WHEN DNS_RESPONSE = 'YXDOMAIN' THEN 6 ELSE 99 END, 99)::NUMBER) WHEN 0 THEN 'NoError' WHEN 1 THEN 'FormError' WHEN 10 THEN 'NotZone' WHEN 11 THEN 'DSOTYPENI' WHEN 16 THEN 'BADSIG_VERS' WHEN 17 THEN 'BADKEY' WHEN 18 THEN 'BADTIME' WHEN 19 THEN 'BADMODE' WHEN 2 THEN 'ServError' WHEN 20 THEN 'BADNAME' WHEN 21 THEN 'BADALG' WHEN 22 THEN 'BADTRUNC' WHEN 23 THEN 'BADCOOKIE' WHEN 24 THEN 'Unassigned' WHEN 25 THEN 'Reserved' WHEN 3 THEN 'NXDomain' WHEN 4 THEN 'NotImp' WHEN 5 THEN 'Refused' WHEN 6 THEN 'YXDomain' WHEN 7 THEN 'YXRRSet' WHEN 8 THEN 'NXRRSet' WHEN 9 THEN 'NotAuth' WHEN 99 THEN 'Other' END``` |
| rcode_id | ```IFF(REGEXP_LIKE(DNS_RESPONSE, '[A-Za-z]+'), CASE WHEN DNS_RESPONSE = 'NOERROR' THEN 0 WHEN DNS_RESPONSE = 'FORMERR' THEN 1 WHEN DNS_RESPONSE = 'SERVFAIL' THEN 2 WHEN DNS_RESPONSE = 'NXDOMAIN' THEN 3 WHEN DNS_RESPONSE = 'NOTIMP' THEN 4 WHEN DNS_RESPONSE = 'REFUSED' THEN 5 WHEN DNS_RESPONSE = 'YXDOMAIN' THEN 6 ELSE 99 END, 99)::NUMBER``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```CLIENT_SOURCE_IP::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (400301::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```400301::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
