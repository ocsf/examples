# Event Dossier: O365 Audit Logs to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `office365`
* Product name: `o365-audit-logs`
* Event codes: `OPERATION in ('UserLoginFailed', 'UserLoggedIn')`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.process.session.uid | ```RECORD_SPECIFIC_DETAILS:device_properties:session_id::VARCHAR``` |
| auth_protocol | ```CASE (CASE WHEN RECORD_SPECIFIC_DETAILS:extended_properties:request_type ILIKE '%OAuth2%' THEN 6 WHEN RECORD_SPECIFIC_DETAILS:extended_properties:request_type ILIKE '%Saml%' THEN 5 WHEN RECORD_SPECIFIC_DETAILS:extended_properties:request_type IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```CASE WHEN RECORD_SPECIFIC_DETAILS:extended_properties:request_type ILIKE '%OAuth2%' THEN 6 WHEN RECORD_SPECIFIC_DETAILS:extended_properties:request_type ILIKE '%Saml%' THEN 5 WHEN RECORD_SPECIFIC_DETAILS:extended_properties:request_type IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| cloud.provider | ```WORKLOAD::VARCHAR``` |
| device.name | ```RECORD_SPECIFIC_DETAILS:device_properties:display_name::VARCHAR``` |
| device.os.name | ```RECORD_SPECIFIC_DETAILS:device_properties:os::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Windows' THEN 100 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Windows Mobile' THEN 101 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Linux' THEN 200 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Android' THEN 201 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='macOS' THEN 300 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='iOS' THEN 301 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='iPadOS' THEN 302 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Solaris' THEN 400 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='AIX' THEN 401 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='HP-UX' THEN 402 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Windows' THEN 100 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Windows Mobile' THEN 101 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Linux' THEN 200 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Android' THEN 201 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='macOS' THEN 300 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='iOS' THEN 301 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='iPadOS' THEN 302 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='Solaris' THEN 400 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='AIX' THEN 401 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os='HP-UX' THEN 402 WHEN RECORD_SPECIFIC_DETAILS:device_properties:os IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| device.uid | ```RECORD_SPECIFIC_DETAILS:device_properties:id::VARCHAR``` |
| http_request.user_agent | ```RECORD_SPECIFIC_DETAILS:extended_properties:user_agent::VARCHAR``` |
| metadata.event_code | ```workload``` |
| metadata.product.name | ```'o365-audit-logs'``` |
| metadata.product.vendor_name | ```'office365'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| status | ```CASE (CASE WHEN RESULT_STATUS IN ('Success', 'Succeeded') THEN 1 WHEN RESULT_STATUS='Failed' THEN 2 WHEN RESULT_STATUS IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_detail | ```RECORD_SPECIFIC_DETAILS:extended_properties:result_status_detail::VARCHAR``` |
| status_id | ```CASE WHEN RESULT_STATUS IN ('Success', 'Succeeded') THEN 1 WHEN RESULT_STATUS='Failed' THEN 2 WHEN RESULT_STATUS IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300201::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300201::NUMBER``` |
| user.credential_uid | ```USER_KEY::VARCHAR``` |
| user.org.uid | ```ORGANIZATION_ID::VARCHAR``` |
| user.type | ```CASE (CASE WHEN USER_TYPE=0 THEN 1 WHEN USER_TYPE=2 THEN 2 WHEN USER_TYPE=4 THEN 3 WHEN USER_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| user.type_id | ```CASE WHEN USER_TYPE=0 THEN 1 WHEN USER_TYPE=2 THEN 2 WHEN USER_TYPE=4 THEN 3 WHEN USER_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| user.uid | ```USER_ID::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
