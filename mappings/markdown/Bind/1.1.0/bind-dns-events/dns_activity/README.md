# Event Dossier: Bind Dns Events to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `bind`
* Product name: `bind-dns-events`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```99::NUMBER``` |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| dst_endpoint.ip | ```DESTINATION_IP::VARCHAR``` |
| metadata.product.name | ```'bind-dns-events'``` |
| metadata.product.vendor_name | ```'bind'``` |
| metadata.version | ```'1.1.0'``` |
| query.class | ```QUERY_CLASS::VARCHAR``` |
| query.hostname | ```QUERY_NAME::VARCHAR``` |
| query.type | ```QUERY_TYPE::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| src_endpoint.port | ```CLIENT_PORT::VARCHAR``` |
| src_endpoint.uid | ```CLIENT_OBJECT_IDENTIFIER::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```to_varchar(event_time::TIMESTAMP_LTZ, 'YYYY-MM-DD"T"HH24:MI:SS.FF3"Z"')``` |
| type_name | ```CASE (400301::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```400301::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
