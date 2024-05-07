# Event Dossier: Netiq Edirectory Audit to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `netiq`
* Product name: `netiq-edirectory-audit`
* Event codes: `EVENT_NAME in ('LOGIN')`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```CASE WHEN EVENT_NAME IS NULL THEN 0 WHEN EVENT_NAME = 'LOGIN' THEN 1 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN EVENT_NAME IS NULL THEN 0 WHEN EVENT_NAME = 'LOGIN' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```SOURCE_USER::VARCHAR``` |
| api.service.name | ```SOURCE_SERVICE_NAME::VARCHAR``` |
| api.service.version | ```SOURCE_PROCESS::VARCHAR``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| device.hostname | ```DEVICE_HOST::VARCHAR``` |
| device.ip | ```DEVICE::VARCHAR``` |
| message | ```RAW:msg::VARCHAR``` |
| metadata.event_code | ```event_name``` |
| metadata.product.name | ```'netiq-edirectory-audit'``` |
| metadata.product.vendor_name | ```'netiq'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (RAW:severity::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```RAW:severity::NUMBER``` |
| src_endpoint.ip | ```COALESCE(RAW:src, SPLIT_PART(INTRUDER_ADDRESS, ':', 2))::VARCHAR``` |
| src_endpoint.port | ```RAW:spt::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', RECEIVED_TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```RECEIVED_TIME::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN OUTCOME IS NULL THEN 0 WHEN OUTCOME = 'Success' THEN 1 WHEN OUTCOME = 'Failure' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN OUTCOME IS NULL THEN 0 WHEN OUTCOME = 'Success' THEN 1 WHEN OUTCOME = 'Failure' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', received_time::TIMESTAMP_LTZ)``` |
| time_dt | ```received_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300200 + CASE WHEN EVENT_NAME IS NULL THEN 0 WHEN EVENT_NAME = 'LOGIN' THEN 1 ELSE 99 END::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300200 + CASE WHEN EVENT_NAME IS NULL THEN 0 WHEN EVENT_NAME = 'LOGIN' THEN 1 ELSE 99 END::NUMBER``` |
| user.name | ```SOURCE_USER::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
