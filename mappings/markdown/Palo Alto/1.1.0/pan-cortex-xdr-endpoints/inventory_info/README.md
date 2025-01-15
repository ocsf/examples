# Event Dossier: Pan Cortex Xdr Endpoints to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `paloalto`
* Product name: `pan-cortex-xdr-endpoints`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Log' WHEN 2 THEN 'Collect' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```USERS[0]::VARCHAR``` |
| category_name | ```CASE (5::NUMBER) WHEN 5 THEN 'Discovery' END``` |
| category_uid | ```5::NUMBER``` |
| class_name | ```'inventory_info'``` |
| class_uid | ```5001``` |
| device.hostname | ```HOST_NAME::VARCHAR``` |
| device.ip | ```IP[0]::VARCHAR``` |
| device.is_managed | ```CASE WHEN OPERATIONAL_STATUS IN ('PROTECTED', 'PARTIALLY_PROTECTED') THEN TRUE ELSE FALSE END::BOOLEAN``` |
| device.last_seen_time | ```date_part('epoch_milliseconds', LAST_SEEN::TIMESTAMP_LTZ)``` |
| device.last_seen_time_dt | ```LAST_SEEN::TIMESTAMP_LTZ``` |
| device.type | ```CASE (CASE WHEN AGENT_TYPE IS NULL THEN 0 WHEN AGENT_TYPE = 'Server' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```CASE WHEN AGENT_TYPE IS NULL THEN 0 WHEN AGENT_TYPE = 'Server' THEN 1 ELSE 99 END::NUMBER``` |
| device.uid | ```AGENT_ID::VARCHAR``` |
| metadata.product.name | ```'pan-cortex-xdr-endpoints'``` |
| metadata.product.vendor_name | ```'paloalto'``` |
| metadata.version | ```'1.1.0'``` |
| time | ```date_part('epoch_milliseconds', last_seen::TIMESTAMP_LTZ)``` |
| time_dt | ```last_seen::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500199::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500199::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
