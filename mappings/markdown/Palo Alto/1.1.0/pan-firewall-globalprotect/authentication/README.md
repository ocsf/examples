# Event Dossier: Pan Firewall Globalprotect to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `paloalto`
* Product name: `pan-firewall-globalprotect`
* Event codes: `EVENT_ID = 'portal-auth'`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| api.response.error | ```ERROR_CODE::VARCHAR``` |
| auth_protocol | ```CASE (CASE WHEN AUTHENTICATION_METHOD IS NULL THEN 0 WHEN AUTHENTICATION_METHOD = 'SAML' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```CASE WHEN AUTHENTICATION_METHOD IS NULL THEN 0 WHEN AUTHENTICATION_METHOD = 'SAML' THEN 5 ELSE 99 END::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| duration | ```(LOGIN_DURATION * 1000)::NUMBER``` |
| metadata.product.name | ```'pan-firewall-globalprotect'``` |
| metadata.product.vendor_name | ```'paloalto'``` |
| metadata.version | ```'1.1.0'``` |
| session.expiration_reason | ```COALESCE(ERROR, REASON)::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.hostname | ```HOST_ID::VARCHAR``` |
| src_endpoint.hw_info.serial_number | ```MACHINE_SERIAL_NUMBER::VARCHAR``` |
| src_endpoint.ip | ```COALESCE(PUBLIC_IP, PUBLIC_IP_V6)::VARCHAR``` |
| src_endpoint.location.region | ```SOURCE_REGION::VARCHAR``` |
| src_endpoint.name | ```MACHINE_NAME::VARCHAR``` |
| src_endpoint.os.name | ```CLIENT_OS::VARCHAR``` |
| src_endpoint.os.type | ```CASE (CASE WHEN CLIENT_OS IS NULL THEN 0 WHEN CLIENT_OS = 'Windows' THEN 100 WHEN CLIENT_OS = 'Linux' THEN 200 WHEN CLIENT_OS = 'Mac' THEN 300 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| src_endpoint.os.type_id | ```CASE WHEN CLIENT_OS IS NULL THEN 0 WHEN CLIENT_OS = 'Windows' THEN 100 WHEN CLIENT_OS = 'Linux' THEN 200 WHEN CLIENT_OS = 'Mac' THEN 300 ELSE 99 END::NUMBER``` |
| src_endpoint.os.version | ```CLIENT_OS_VERSION::VARCHAR``` |
| status | ```CASE (CASE WHEN STATUS IS NULL THEN 0 WHEN STATUS = 'success' THEN 1 WHEN STATUS = 'failure' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS IS NULL THEN 0 WHEN STATUS = 'success' THEN 1 WHEN STATUS = 'failure' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', generated_time::TIMESTAMP_LTZ)``` |
| time_dt | ```generated_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300201::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300201::NUMBER``` |
| user.name | ```SOURCE_USER::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
