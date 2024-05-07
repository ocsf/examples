# Event Dossier: Jamf Computers to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `jamf`
* Product name: `jamf-computers`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```99::NUMBER``` |
| activity_name | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Log' WHEN 2 THEN 'Collect' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (5::NUMBER) WHEN 5 THEN 'Discovery' END``` |
| category_uid | ```5::NUMBER``` |
| class_name | ```'inventory_info'``` |
| class_uid | ```5001``` |
| device.first_seen_time | ```date_part('epoch_milliseconds', GENERAL_INITIAL_ENTRY_DATE_UTC::TIMESTAMP_LTZ)``` |
| device.first_seen_time_dt | ```GENERAL_INITIAL_ENTRY_DATE_UTC::TIMESTAMP_LTZ``` |
| device.hw_info.bios_manufacturer | ```HARDWARE_MAKE::VARCHAR``` |
| device.hw_info.cpu_cores | ```HARDWARE:number_cores::NUMBER``` |
| device.hw_info.cpu_count | ```HARDWARE:number_processors::NUMBER``` |
| device.hw_info.cpu_speed | ```COALESCE(HARDWARE:processor_speed::NUMBER, HARDWARE:processor_speed_mhz::NUMBER)::NUMBER``` |
| device.hw_info.cpu_type | ```HARDWARE:processor_type::VARCHAR``` |
| device.hw_info.ram_size | ```COALESCE(HARDWARE:total_ram::NUMBER, HARDWARE:total_ram_mb::NUMBER)::NUMBER``` |
| device.hw_info.serial_number | ```GENERAL_SERIAL_NUMBER::VARCHAR``` |
| device.ip | ```COALESCE(GENERAL_IP_ADDRESS::VARCHAR, GENERAL_LAST_REPORTED_IP::VARCHAR)::VARCHAR``` |
| device.is_managed | ```GENERAL_REMOTE_MANAGEMENT:manage::BOOLEAN``` |
| device.last_seen_time | ```date_part('epoch_milliseconds', GENERAL_LAST_ENROLLED_DATE_UTC::TIMESTAMP_LTZ)``` |
| device.last_seen_time_dt | ```GENERAL_LAST_ENROLLED_DATE_UTC::TIMESTAMP_LTZ``` |
| device.location.city | ```LOCATION:building::VARCHAR``` |
| device.location.provider | ```LOCATION:department::VARCHAR``` |
| device.mac | ```COALESCE(GENERAL_MAC_ADDRESS::VARCHAR, GENERAL_ALT_MAC_ADDRESS::VARCHAR)::VARCHAR``` |
| device.modified_time | ```date_part('epoch_milliseconds', GENERAL_LAST_CONTACT_TIME_UTC::TIMESTAMP_LTZ)``` |
| device.modified_time_dt | ```GENERAL_LAST_CONTACT_TIME_UTC::TIMESTAMP_LTZ``` |
| device.name | ```GENERAL_NAME::VARCHAR``` |
| device.network_interfaces | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('type', CASE (CASE WHEN GENERAL_NETWORK_ADAPTER_TYPE IS NULL THEN 0 WHEN GENERAL_NETWORK_ADAPTER_TYPE = 'Ethernet' THEN 1 WHEN GENERAL_NETWORK_ADAPTER_TYPE = 'IEEE80211' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Wired' WHEN 2 THEN 'Wireless' WHEN 3 THEN 'Mobile' WHEN 4 THEN 'Tunnel' WHEN 99 THEN 'Other' END, 'type_id', CASE WHEN GENERAL_NETWORK_ADAPTER_TYPE IS NULL THEN 0 WHEN GENERAL_NETWORK_ADAPTER_TYPE = 'Ethernet' THEN 1 WHEN GENERAL_NETWORK_ADAPTER_TYPE = 'IEEE80211' THEN 2 ELSE 99 END::NUMBER))``` |
| device.os.build | ```HARDWARE_OS_BUILD::VARCHAR``` |
| device.os.name | ```GENERAL_PLATFORM::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN HARDWARE_OS_NAME IS NULL THEN 0 WHEN HARDWARE_OS_NAME = 'macOS' THEN 300 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN HARDWARE_OS_NAME IS NULL THEN 0 WHEN HARDWARE_OS_NAME = 'macOS' THEN 300 ELSE 99 END::NUMBER``` |
| device.os.version | ```HARDWARE_OS_VERSION::VARCHAR``` |
| device.region | ```GENERAL_SITE:name::VARCHAR``` |
| device.type | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```0::NUMBER``` |
| device.uid | ```GENERAL_UDID::VARCHAR``` |
| metadata.product.name | ```'jamf-computers'``` |
| metadata.product.vendor_name | ```'jamf'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| time | ```date_part('epoch_milliseconds', sample_time::TIMESTAMP_LTZ)``` |
| time_dt | ```sample_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500199::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500199::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
