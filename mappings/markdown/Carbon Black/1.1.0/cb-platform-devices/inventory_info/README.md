# Event Dossier: Cb Platform Devices to OCSF class Inventory Info

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `inventory_info`
* Vendor name: `cb-defense`
* Product name: `cb-platform-devices`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```2::NUMBER``` |
| activity_name | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Log' WHEN 2 THEN 'Collect' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```EMAIL::VARCHAR``` |
| actor.user.name | ```LOGIN_USER_NAME::VARCHAR``` |
| category_name | ```CASE (5::NUMBER) WHEN 5 THEN 'Discovery' END``` |
| category_uid | ```5::NUMBER``` |
| class_name | ```'inventory_info'``` |
| class_uid | ```5001``` |
| device.created_time | ```date_part('epoch_milliseconds', REGISTERED_TIME::TIMESTAMP_LTZ)``` |
| device.created_time_dt | ```REGISTERED_TIME::TIMESTAMP_LTZ``` |
| device.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('uid', AD_GROUP_ID::VARCHAR))``` |
| device.hostname | ```NAME::VARCHAR``` |
| device.hypervisor | ```VIRTUALIZATION_PROVIDER::VARCHAR``` |
| device.instance_uid | ```VM_UUID::VARCHAR``` |
| device.ip | ```LAST_EXTERNAL_IP_ADDRESS::VARCHAR``` |
| device.last_seen_time | ```date_part('epoch_milliseconds', LAST_CONTACT_TIME::TIMESTAMP_LTZ)``` |
| device.last_seen_time_dt | ```LAST_CONTACT_TIME::TIMESTAMP_LTZ``` |
| device.location.region | ```LAST_LOCATION::VARCHAR``` |
| device.mac | ```MAC_ADDRESS::VARCHAR``` |
| device.modified_time | ```date_part('epoch_milliseconds', COALESCE(LAST_DEVICE_POLICY_CHANGE_TIME, LAST_POLICY_UPDATED_TIME)::TIMESTAMP_LTZ)``` |
| device.modified_time_dt | ```COALESCE(LAST_DEVICE_POLICY_CHANGE_TIME, LAST_POLICY_UPDATED_TIME)::TIMESTAMP_LTZ``` |
| device.org.name | ```ORGANIZATION_NAME::VARCHAR``` |
| device.org.uid | ```ORGANIZATION_ID::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN OS IS NULL THEN 0 WHEN OS = 'WINDOWS' THEN 100 WHEN OS = 'LINUX' THEN 200 WHEN OS = 'MAC' THEN 300 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS IS NULL THEN 0 WHEN OS = 'WINDOWS' THEN 100 WHEN OS = 'LINUX' THEN 200 WHEN OS = 'MAC' THEN 300 ELSE 99 END::NUMBER``` |
| device.os.version | ```OS_VERSION::VARCHAR``` |
| device.uid | ```ID::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', SCAN_LAST_COMPLETE_TIME::TIMESTAMP_LTZ)``` |
| end_time_dt | ```SCAN_LAST_COMPLETE_TIME::TIMESTAMP_LTZ``` |
| metadata.product.name | ```'cb-platform-devices'``` |
| metadata.product.vendor_name | ```'cb-defense'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN VULNERABILITY_SEVERITY IS NULL THEN 0 WHEN VULNERABILITY_SEVERITY = 'LOW' THEN 2 WHEN VULNERABILITY_SEVERITY = 'MODERATE' THEN 3 WHEN VULNERABILITY_SEVERITY = 'IMPORTANT' THEN 4 WHEN VULNERABILITY_SEVERITY = 'CRITICAL' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN VULNERABILITY_SEVERITY IS NULL THEN 0 WHEN VULNERABILITY_SEVERITY = 'LOW' THEN 2 WHEN VULNERABILITY_SEVERITY = 'MODERATE' THEN 3 WHEN VULNERABILITY_SEVERITY = 'IMPORTANT' THEN 4 WHEN VULNERABILITY_SEVERITY = 'CRITICAL' THEN 5 ELSE 99 END::NUMBER``` |
| start_time | ```date_part('epoch_milliseconds', SCAN_LAST_ACTION_TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```SCAN_LAST_ACTION_TIME::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN STATUS IS NULL THEN 0 WHEN STATUS IN ('REGISTERED', 'DEREGISTERED', 'BYPASS') THEN 1 WHEN STATUS IN ('PENDING') THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS IS NULL THEN 0 WHEN STATUS IN ('REGISTERED', 'DEREGISTERED', 'BYPASS') THEN 1 WHEN STATUS IN ('PENDING') THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', last_contact_time::TIMESTAMP_LTZ)``` |
| time_dt | ```last_contact_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (500102::NUMBER) WHEN 500100 THEN 'Device Inventory Info: Unknown' WHEN 500101 THEN 'Device Inventory Info: Log' WHEN 500102 THEN 'Device Inventory Info: Collect' WHEN 500199 THEN 'Device Inventory Info: Other' END``` |
| type_uid | ```500102::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
