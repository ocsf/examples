# Event Dossier: Island Browser Devices to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `Island`
* Product name: `island-browser-devices`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```2::NUMBER``` |
| activity_name | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Log' WHEN 2 THEN 'Collect' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```EMAIL::VARCHAR``` |
| actor.user.name | ```USER_NAME::VARCHAR``` |
| actor.user.uid | ```USER_ID::VARCHAR``` |
| category_name | ```CASE (5::NUMBER) WHEN 5 THEN 'Discovery' END``` |
| category_uid | ```5::NUMBER``` |
| class_name | ```'inventory_info'``` |
| class_uid | ```5001``` |
| device.hw_info.cpu_type | ```CPU_MODEL::VARCHAR``` |
| device.hw_info.ram_size | ```RAM_SIZE::NUMBER``` |
| device.hw_info.serial_number | ```SERIAL_NUMBER::VARCHAR``` |
| device.ip | ```EXTERNAL_IP_ADDRESS::VARCHAR``` |
| device.last_seen_time | ```date_part('epoch_milliseconds', LAST_SEEN::TIMESTAMP_LTZ)``` |
| device.last_seen_time_dt | ```LAST_SEEN::TIMESTAMP_LTZ``` |
| device.mac | ```MAC_ADDRESS::VARCHAR``` |
| device.name | ```MACHINE_NAME::VARCHAR``` |
| device.os.name | ```OS_PLATFORM::VARCHAR``` |
| device.os.version | ```OS_VERSION::VARCHAR``` |
| device.uid | ```MACHINE_ID::VARCHAR``` |
| metadata.product.name | ```'island-browser-devices'``` |
| metadata.product.vendor_name | ```'Island'``` |
| metadata.tenant_uid | ```TENANT_ID::VARCHAR``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', created_date::TIMESTAMP_LTZ)``` |
| time_dt | ```created_date::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500102::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500102::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
