# Event Dossier: Sentinelone Agents to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `sentinelone`
* Product name: `sentinelone-agents`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Log' WHEN 2 THEN 'Collect' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (5::NUMBER) WHEN 5 THEN 'Discovery' END``` |
| category_uid | ```5::NUMBER``` |
| class_name | ```'inventory_info'``` |
| class_uid | ```5001``` |
| device.created_time | ```date_part('epoch_milliseconds', CREATED_AT::TIMESTAMP_LTZ)``` |
| device.created_time_dt | ```CREATED_AT::TIMESTAMP_LTZ``` |
| device.domain | ```DOMAIN::VARCHAR``` |
| device.first_seen_time | ```date_part('epoch_milliseconds', REGISTERED_AT::TIMESTAMP_LTZ)``` |
| device.first_seen_time_dt | ```REGISTERED_AT::TIMESTAMP_LTZ``` |
| device.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', GROUP_NAME::VARCHAR))``` |
| device.hostname | ```COMPUTER_NAME::VARCHAR``` |
| device.hw_info.cpu_cores | ```RAW:coreCount::NUMBER``` |
| device.hw_info.cpu_count | ```RAW:cpuCount::NUMBER``` |
| device.hw_info.ram_size | ```RAW:totalMemory::NUMBER``` |
| device.hw_info.serial_number | ```RAW:serialNumber::VARCHAR``` |
| device.ip | ```EXTERNAL_IP::VARCHAR``` |
| device.last_seen_time | ```date_part('epoch_milliseconds', LAST_ACTIVE_DATE::TIMESTAMP_LTZ)``` |
| device.last_seen_time_dt | ```LAST_ACTIVE_DATE::TIMESTAMP_LTZ``` |
| device.modified_time | ```date_part('epoch_milliseconds', UPDATED_AT::TIMESTAMP_LTZ)``` |
| device.modified_time_dt | ```UPDATED_AT::TIMESTAMP_LTZ``` |
| device.name | ```MODEL_NAME::VARCHAR``` |
| device.network_interfaces | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('ip', NETWORK_INTERFACES[0].gatewayIp::VARCHAR, 'mac', NETWORK_INTERFACES[0].gatewayMacAddress::VARCHAR, 'name', NETWORK_INTERFACES[0].name::VARCHAR, 'uid', NETWORK_INTERFACES[0].id::VARCHAR))``` |
| device.os.name | ```OS_NAME::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN OS_TYPE IS NULL THEN 0 WHEN OS_TYPE = 'windows' THEN 100 WHEN OS_TYPE = 'linux' THEN 200 WHEN OS_TYPE = 'macos' THEN 300 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS_TYPE IS NULL THEN 0 WHEN OS_TYPE = 'windows' THEN 100 WHEN OS_TYPE = 'linux' THEN 200 WHEN OS_TYPE = 'macos' THEN 300 ELSE 99 END::NUMBER``` |
| device.type | ```CASE (CASE WHEN MACHINE_TYPE IS NULL THEN 0 WHEN MACHINE_TYPE = 'server' THEN 1 WHEN MACHINE_TYPE = 'desktop' THEN 2 WHEN MACHINE_TYPE = 'laptop' THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```CASE WHEN MACHINE_TYPE IS NULL THEN 0 WHEN MACHINE_TYPE = 'server' THEN 1 WHEN MACHINE_TYPE = 'desktop' THEN 2 WHEN MACHINE_TYPE = 'laptop' THEN 3 ELSE 99 END::NUMBER``` |
| device.uid | ```UUID::VARCHAR``` |
| device.uid_alt | ```ID::VARCHAR``` |
| metadata.product.name | ```'sentinelone-agents'``` |
| metadata.product.vendor_name | ```'sentinelone'``` |
| metadata.version | ```'1.1.0'``` |
| time | ```date_part('epoch_milliseconds', last_active_date::TIMESTAMP_LTZ)``` |
| time_dt | ```last_active_date::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500101::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500101::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
