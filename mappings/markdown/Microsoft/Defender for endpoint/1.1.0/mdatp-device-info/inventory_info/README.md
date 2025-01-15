# Event Dossier: Mdatp Device Info to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `mdatp`
* Product name: `mdatp-device-info`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```2::NUMBER``` |
| activity_name | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Log' WHEN 2 THEN 'Collect' WHEN 99 THEN 'Other' END``` |
| actor.session.uid | ```PARSE_JSON(LOGGED_ON_USERS[0])[0]:Sid::VARCHAR``` |
| actor.user.name | ```PARSE_JSON(LOGGED_ON_USERS[0])[0]:UserName::VARCHAR``` |
| category_name | ```CASE (5::NUMBER) WHEN 5 THEN 'Discovery' END``` |
| category_uid | ```5::NUMBER``` |
| class_name | ```'inventory_info'``` |
| class_uid | ```5001``` |
| device.container.tag | ```REGISTRY_DEVICE_TAG::VARCHAR``` |
| device.domain | ```PARSE_JSON(LOGGED_ON_USERS[0])[0]:DomainName::VARCHAR``` |
| device.groups | ```ARRAY_CONSTRUCT(MACHINE_GROUP)``` |
| device.ip | ```PUBLIC_IP::VARCHAR``` |
| device.name | ```DEVICE_NAME::VARCHAR``` |
| device.os.build | ```OS_BUILD::VARCHAR``` |
| device.os.cpu_bits | ```CASE WHEN OS_ARCHITECTURE ILIKE '%64%' THEN 64 WHEN OS_ARCHITECTURE ILIKE '%32%' THEN 32 ELSE NULL END::NUMBER``` |
| device.os.type | ```CASE (CASE WHEN OS_PLATFORM ILIKE '%Windows%' THEN 100 WHEN OS_PLATFORM = 'Linux' THEN 200 WHEN OS_PLATFORM = 'macOS' THEN 300 WHEN OS_PLATFORM = 'Android' THEN 201 WHEN OS_PLATFORM = 'iOS' THEN 301 WHEN OS_PLATFORM IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS_PLATFORM ILIKE '%Windows%' THEN 100 WHEN OS_PLATFORM = 'Linux' THEN 200 WHEN OS_PLATFORM = 'macOS' THEN 300 WHEN OS_PLATFORM = 'Android' THEN 201 WHEN OS_PLATFORM = 'iOS' THEN 301 WHEN OS_PLATFORM IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| device.os.version | ```OS_VERSION::VARCHAR``` |
| device.uid | ```DEVICE_ID::VARCHAR``` |
| metadata.product.name | ```'mdatp-device-info'``` |
| metadata.product.vendor_name | ```'mdatp'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```99::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500199::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500199::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
