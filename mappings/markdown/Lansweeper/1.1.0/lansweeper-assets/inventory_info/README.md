# Event Dossier: Lansweeper Assets to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `lansweeper`
* Product name: `lansweeper-assets`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```0::NUMBER``` |
| activity_name | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Log' WHEN 2 THEN 'Collect' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (5::NUMBER) WHEN 5 THEN 'Discovery' END``` |
| category_uid | ```5::NUMBER``` |
| class_name | ```'inventory_info'``` |
| class_uid | ```5001``` |
| device.first_seen_time | ```date_part('epoch_milliseconds', FIRST_SEEN::TIMESTAMP_LTZ)``` |
| device.first_seen_time_dt | ```FIRST_SEEN::TIMESTAMP_LTZ``` |
| device.ip | ```IP_ADDRESS::VARCHAR``` |
| device.last_seen_time | ```date_part('epoch_milliseconds', LAST_SEEN::TIMESTAMP_LTZ)``` |
| device.last_seen_time_dt | ```LAST_SEEN::TIMESTAMP_LTZ``` |
| device.mac | ```MAC::VARCHAR``` |
| device.name | ```NAME::VARCHAR``` |
| device.type | ```CASE (CASE WHEN TYPE = 'Server' THEN 1 WHEN TYPE = 'Desktop' THEN 2 WHEN TYPE = 'Laptop' THEN 3 WHEN TYPE = 'Tablet' THEN 4 WHEN TYPE = 'Mobile' THEN 5 WHEN TYPE = 'Virtual' THEN 6 WHEN TYPE = 'IOT' THEN 7 WHEN TYPE = 'Browser' THEN 8 WHEN TYPE = 'Firewall' THEN 9 WHEN TYPE = 'Switch' THEN 10 WHEN TYPE = 'Hub' THEN 11 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```CASE WHEN TYPE = 'Server' THEN 1 WHEN TYPE = 'Desktop' THEN 2 WHEN TYPE = 'Laptop' THEN 3 WHEN TYPE = 'Tablet' THEN 4 WHEN TYPE = 'Mobile' THEN 5 WHEN TYPE = 'Virtual' THEN 6 WHEN TYPE = 'IOT' THEN 7 WHEN TYPE = 'Browser' THEN 8 WHEN TYPE = 'Firewall' THEN 9 WHEN TYPE = 'Switch' THEN 10 WHEN TYPE = 'Hub' THEN 11 ELSE 99 END::NUMBER``` |
| device.uid | ```KEY::VARCHAR``` |
| metadata.product.name | ```'lansweeper-assets'``` |
| metadata.product.vendor_name | ```'lansweeper'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', SNAPSHOT_TIME::TIMESTAMP_LTZ)``` |
| time_dt | ```SNAPSHOT_TIME::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500100::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500100::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
