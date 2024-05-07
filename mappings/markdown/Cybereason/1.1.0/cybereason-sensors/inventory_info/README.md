# Event Dossier: Cybereason Sensors to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `Cybereason`
* Product name: `cybereason-sensors`
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
| device.domain | ```FQDN::VARCHAR``` |
| device.first_seen_time | ```date_part('epoch_milliseconds', FIRST_SEEN_TIME::TIMESTAMP_LTZ)``` |
| device.first_seen_time_dt | ```FIRST_SEEN_TIME::TIMESTAMP_LTZ``` |
| device.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('name', GROUP_NAME::VARCHAR, 'uid', GROUP_ID::VARCHAR))``` |
| device.ip | ```EXTERNAL_IP_ADDRESS::VARCHAR``` |
| device.last_seen_time | ```date_part('epoch_milliseconds', DISCONNECTION_TIME::TIMESTAMP_LTZ)``` |
| device.last_seen_time_dt | ```DISCONNECTION_TIME::TIMESTAMP_LTZ``` |
| device.modified_time | ```date_part('epoch_milliseconds', SENSOR_LAST_UPDATE::TIMESTAMP_LTZ)``` |
| device.modified_time_dt | ```SENSOR_LAST_UPDATE::TIMESTAMP_LTZ``` |
| device.name | ```MACHINE_NAME::VARCHAR``` |
| device.org.name | ```ORGANIZATION::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN OS_TYPE='Windows' THEN 100 WHEN OS_TYPE='Windows Mobile' THEN 101 WHEN OS_TYPE='Linux' THEN 200 WHEN OS_TYPE='Android' THEN 201 WHEN OS_TYPE='macOS' THEN 300 WHEN OS_TYPE='iOS' THEN 301 WHEN OS_TYPE='iPadOS' THEN 302 WHEN OS_TYPE='Solaris' THEN 400 WHEN OS_TYPE='AIX' THEN 401 WHEN OS_TYPE='HP-UX' THEN 402 WHEN STATUS IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS_TYPE='Windows' THEN 100 WHEN OS_TYPE='Windows Mobile' THEN 101 WHEN OS_TYPE='Linux' THEN 200 WHEN OS_TYPE='Android' THEN 201 WHEN OS_TYPE='macOS' THEN 300 WHEN OS_TYPE='iOS' THEN 301 WHEN OS_TYPE='iPadOS' THEN 302 WHEN OS_TYPE='Solaris' THEN 400 WHEN OS_TYPE='AIX' THEN 401 WHEN OS_TYPE='HP-UX' THEN 402 WHEN STATUS IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| device.os.version | ```OS_VERSION_TYPE::VARCHAR``` |
| device.type | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```0::NUMBER``` |
| device.uid | ```SENSOR_ID::VARCHAR``` |
| device.uid_alt | ```GUID::VARCHAR``` |
| metadata.product.name | ```'cybereason-sensors'``` |
| metadata.product.vendor_name | ```'Cybereason'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| status | ```CASE (CASE WHEN STATUS='Success' THEN 1 WHEN STATUS='Failure' THEN 2 WHEN STATUS IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS='Success' THEN 1 WHEN STATUS='Failure' THEN 2 WHEN STATUS IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', LAST_PYLUM_UPDATE_TIMESTAMP_MS::TIMESTAMP_LTZ)``` |
| time_dt | ```LAST_PYLUM_UPDATE_TIMESTAMP_MS::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500100::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500100::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
