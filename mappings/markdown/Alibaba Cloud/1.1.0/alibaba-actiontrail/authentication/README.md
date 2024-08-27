# Event Dossier: Alibaba Actiontrail to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `alibaba`
* Product name: `alibaba-actiontrail`
* Event codes: `EVENT_NAME = 'ConsoleSignin'`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.user.account.uid | ```RECIPIENT_ACCOUNT_ID::VARCHAR``` |
| api.response.error | ```ERROR_CODE::VARCHAR``` |
| api.response.error_message | ```ERROR_MESSAGE::VARCHAR``` |
| auth_protocol | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```0::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| cloud.provider | ```'Alibaba'::VARCHAR``` |
| cloud.region | ```ACS_REGION::VARCHAR``` |
| dst_endpoint.hostname | ```EVENT_SOURCE::VARCHAR``` |
| enrichments.name | ```EVENT_NAME::VARCHAR``` |
| http_request.length | ```REQUEST_PARAMETERS_LENGTH::NUMBER``` |
| http_request.uid | ```REQUEST_ID::VARCHAR``` |
| http_request.url.query_string | ```SPLIT_PART(ADDITIONAL_EVENT_DATA:callbackUrl, '?', 2)::VARCHAR``` |
| http_request.url.scheme | ```REGEXP_SUBSTR(ADDITIONAL_EVENT_DATA:callbackUrl, '^([a-zA-Z]+)')::VARCHAR``` |
| http_request.url.url_string | ```ADDITIONAL_EVENT_DATA:callbackUrl::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| is_cleartext | ```IFF(REGEXP_SUBSTR(ADDITIONAL_EVENT_DATA:callbackUrl, '^([a-zA-Z]+)') != 'https', 'true', 'false')::BOOLEAN``` |
| is_mfa | ```USER_IDENTITY_SESSION_CONTEXT_ATTRIBUTES:mfaAuthenticated::BOOLEAN``` |
| logon_type | ```CASE (3::NUMBER) WHEN 0 THEN 'System' WHEN 10 THEN 'Remote Interactive' WHEN 11 THEN 'Cached Interactive' WHEN 12 THEN 'Cached Remote Interactive' WHEN 13 THEN 'Cached Unlock' WHEN 2 THEN 'Interactive' WHEN 3 THEN 'Network' WHEN 4 THEN 'Batch' WHEN 5 THEN 'OS Service' WHEN 7 THEN 'Unlock' WHEN 8 THEN 'Network Cleartext' WHEN 9 THEN 'New Credentials' WHEN 99 THEN 'Other' END``` |
| logon_type_id | ```3::NUMBER``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'alibaba-actiontrail'``` |
| metadata.product.vendor_name | ```'alibaba'``` |
| metadata.version | ```'1.1.0'``` |
| service.name | ```SERVICE_NAME::VARCHAR``` |
| service.version | ```EVENT_VERSION::VARCHAR``` |
| session.is_mfa | ```ADDITIONAL_EVENT_DATA:mfaChecked::BOOLEAN``` |
| session.uid | ```EVENT_ID::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```SOURCE_IP_ADDRESS::VARCHAR``` |
| src_endpoint.vpc_uid | ```REQUEST_PARAMETERS_CLIENT_VPC_ID::VARCHAR``` |
| status | ```CASE (CASE WHEN COALESCE(ERROR_CODE, ERROR_MESSAGE) IS NULL THEN 1 WHEN COALESCE(ERROR_CODE, ERROR_MESSAGE) IS NOT NULL THEN 2 WHEN ERROR_CODE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN COALESCE(ERROR_CODE, ERROR_MESSAGE) IS NULL THEN 1 WHEN COALESCE(ERROR_CODE, ERROR_MESSAGE) IS NOT NULL THEN 2 WHEN ERROR_CODE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300201::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300201::NUMBER``` |
| user.account.uid | ```USER_IDENTITY_ACCOUNT_ID::VARCHAR``` |
| user.credential_uid | ```USER_IDENTITY_ACCESS_KEY_ID::VARCHAR``` |
| user.name | ```USER_IDENTITY_USER_NAME::VARCHAR``` |
| user.type | ```CASE (CASE WHEN USER_IDENTITY_TYPE = 'ram-user' THEN 1 WHEN USER_IDENTITY_TYPE = 'root-account' THEN 2 WHEN USER_IDENTITY_TYPE = 'system' THEN 3 WHEN USER_IDENTITY_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| user.type_id | ```CASE WHEN USER_IDENTITY_TYPE = 'ram-user' THEN 1 WHEN USER_IDENTITY_TYPE = 'root-account' THEN 2 WHEN USER_IDENTITY_TYPE = 'system' THEN 3 WHEN USER_IDENTITY_TYPE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| user.uid_alt | ```USER_IDENTITY_PRINCIPAL_ID::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
