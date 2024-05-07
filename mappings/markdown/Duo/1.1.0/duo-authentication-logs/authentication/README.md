# Event Dossier: Duo Authentication Logs to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `duo`
* Product name: `duo-authentication-logs`
* Event codes: `EVENT_TYPE = 'authentication'`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```CASE WHEN RESULT IS NULL THEN 0 WHEN RESULT = 'success' THEN 1 WHEN RESULT = 'denied' THEN 2 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN RESULT IS NULL THEN 0 WHEN RESULT = 'success' THEN 1 WHEN RESULT = 'denied' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| device.hostname | ```ACCESS_DEVICE_HOSTNAME::VARCHAR``` |
| device.ip | ```ACCESS_DEVICE_IP::VARCHAR``` |
| device.location.city | ```AUTH_DEVICE_LOCATION:city::VARCHAR``` |
| device.location.country | ```AUTH_DEVICE_LOCATION:country::VARCHAR``` |
| device.os.name | ```ACCESS_DEVICE_OS::VARCHAR``` |
| device.os.version | ```CONCAT(ACCESS_DEVICE_OS, ' ', RAW:access_device:os_version)::VARCHAR``` |
| device.type | ```CASE (CASE WHEN ACCESS_DEVICE_BROWSER IS NULL THEN 0 ELSE 8 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```CASE WHEN ACCESS_DEVICE_BROWSER IS NULL THEN 0 ELSE 8 END::NUMBER``` |
| device.uid | ```ACCESS_DEVICE_EPKEY::VARCHAR``` |
| is_mfa | ```IFF(FACTOR IS NULL OR FACTOR = 'not_available', false, true)::BOOLEAN``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'duo-authentication-logs'``` |
| metadata.product.vendor_name | ```'duo'``` |
| metadata.version | ```'1.1.0'``` |
| service.name | ```APPLICATION_NAME::VARCHAR``` |
| service.uid | ```APPLICATION_KEY::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.hostname | ```HOST::VARCHAR``` |
| status | ```CASE (CASE WHEN RESULT IS NULL THEN 0 WHEN RESULT = 'success' THEN 1 WHEN RESULT = 'denied' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_detail | ```REASON::VARCHAR``` |
| status_id | ```CASE WHEN RESULT IS NULL THEN 0 WHEN RESULT = 'success' THEN 1 WHEN RESULT = 'denied' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((300200 + (CASE WHEN RESULT IS NULL THEN 0 WHEN RESULT = 'success' THEN 1 WHEN RESULT = 'denied' THEN 2 ELSE 99 END))::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```(300200 + (CASE WHEN RESULT IS NULL THEN 0 WHEN RESULT = 'success' THEN 1 WHEN RESULT = 'denied' THEN 2 ELSE 99 END))::NUMBER``` |
| user.email_addr | ```EMAIL::VARCHAR``` |
| user.groups | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT('name', USER_GROUPS[0]))::VARIANT``` |
| user.name | ```USER_NAME::VARCHAR``` |
| user.uid | ```USER_KEY::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
