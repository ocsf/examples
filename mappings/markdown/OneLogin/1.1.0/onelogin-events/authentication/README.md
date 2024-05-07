# Event Dossier: Onelogin Events to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `OneLogin`
* Product name: `onelogin-events`
* Event codes: `EVENT_TYPE_ID IN (5, 6)`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.user.account.uid | ```ACCOUNT_ID::VARCHAR``` |
| actor.user.name | ```COALESCE(ACTOR_USER_NAME, ACTOR_SYSTEM)::VARCHAR``` |
| actor.user.uid | ```COALESCE(ACTOR_USER_ID, ASSUMING_ACTING_USER_ID)::VARCHAR``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| device.name | ```OTP_DEVICE_NAME::VARCHAR``` |
| device.uid | ```OTP_DEVICE_ID::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| metadata.product.name | ```'onelogin-events'``` |
| metadata.product.vendor_name | ```'OneLogin'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```IPADDR::VARCHAR``` |
| src_endpoint.uid | ```RAW:event:client_id::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300201::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300201::NUMBER``` |
| user.name | ```USER_NAME::VARCHAR``` |
| user.uid | ```USER_ID::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
