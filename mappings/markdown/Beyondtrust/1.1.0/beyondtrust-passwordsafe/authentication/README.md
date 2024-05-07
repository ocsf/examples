# Event Dossier: Beyondtrust Passwordsafe to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `beyondtrust`
* Product name: `beyondtrust-passwordsafe`
* Event codes: `EVENT_NAME = 'Login'`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```CASE WHEN ACTION_TYPE = 'Login' THEN 1 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION_TYPE = 'Login' THEN 1 WHEN ACTION_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| auth_protocol | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```0::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| device.uid | ```AGENT_ID::VARCHAR``` |
| dst_endpoint.hostname | ```HOST_NAME::VARCHAR``` |
| dst_endpoint.ip | ```IP_ADDRESS::VARCHAR``` |
| logon_type | ```CASE (3::NUMBER) WHEN 0 THEN 'System' WHEN 10 THEN 'Remote Interactive' WHEN 11 THEN 'Cached Interactive' WHEN 12 THEN 'Cached Remote Interactive' WHEN 13 THEN 'Cached Unlock' WHEN 2 THEN 'Interactive' WHEN 3 THEN 'Network' WHEN 4 THEN 'Batch' WHEN 5 THEN 'OS Service' WHEN 7 THEN 'Unlock' WHEN 8 THEN 'Network Cleartext' WHEN 9 THEN 'New Credentials' WHEN 99 THEN 'Other' END``` |
| logon_type_id | ```3::NUMBER``` |
| message | ```MESSAGE::VARCHAR``` |
| metadata.event_code | ```EVENT_NAME``` |
| metadata.product.name | ```'beyondtrust-passwordsafe'``` |
| metadata.product.vendor_name | ```'beyondtrust'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.hostname | ```SOURCE_HOST::VARCHAR``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| status | ```CASE (CASE WHEN MESSAGE IS NULL THEN 1 WHEN MESSAGE IS NOT NULL THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_detail | ```COALESCE(CATEGORY, SYSTEM_NAME)::VARCHAR``` |
| status_id | ```CASE WHEN MESSAGE IS NULL THEN 1 WHEN MESSAGE IS NOT NULL THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', time::TIMESTAMP_LTZ)``` |
| time_dt | ```time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN ACTION_TYPE = 'Login' THEN 300201 WHEN ACTION_TYPE IS NULL THEN 300200 ELSE 300299 END::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```CASE WHEN ACTION_TYPE = 'Login' THEN 300201 WHEN ACTION_TYPE IS NULL THEN 300200 ELSE 300299 END::NUMBER``` |
| user.account.name | ```ACCOUNT_NAME::VARCHAR``` |
| user.account.uid | ```APP_USER_ID::VARCHAR``` |
| user.credential_uid | ```API_KEY::VARCHAR``` |
| user.name | ```USER_NAME::VARCHAR``` |
| user.uid | ```USER_ID::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
