# Event Dossier: Oracle Audit Logs to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `oracle`
* Product name: `oracle-audit-logs`
* Event codes: `EVENT_NAME in ('InteractiveLogin', 'ReceiveSamlSpSsoResonse')`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| api.group.uid | ```EVENT_GROUPING_ID::VARCHAR``` |
| api.operation | ```ACTION::VARCHAR``` |
| api.response.code | ```STATUS::NUMBER``` |
| api.response.data | ```RESPONSE::VARIANT``` |
| api.response.message | ```MESSAGE::VARCHAR``` |
| auth_protocol | ```CASE (CASE WHEN ADDITIONAL_DETAILS:ssoIdentityProviderType = 'SAML' THEN 5 WHEN ADDITIONAL_DETAILS:ssoIdentityProviderType IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```CASE WHEN ADDITIONAL_DETAILS:ssoIdentityProviderType = 'SAML' THEN 5 WHEN ADDITIONAL_DETAILS:ssoIdentityProviderType IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| cloud.account.uid | ```TENANT_ID::VARCHAR``` |
| cloud.provider | ```'Oracle'::VARCHAR``` |
| cloud.region | ```AVAILABILITY_DOMAIN::VARCHAR``` |
| http_request.http_method | ```CASE WHEN ACTION = 'CONNECT' THEN 'CONNECT' WHEN ACTION = 'DELETE' THEN 'DELETE' WHEN ACTION = 'GET' THEN 'GET' WHEN ACTION = 'HEAD' THEN 'HEAD' WHEN ACTION = 'OPTIONS' THEN 'OPTIONS' WHEN ACTION = 'POST' THEN 'POST' WHEN ACTION = 'PUT' THEN 'PUT' WHEN ACTION = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.uid | ```REQUEST_ID::VARCHAR``` |
| http_request.url.path | ```REQUEST_PATH::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| logon_type | ```CASE (3::NUMBER) WHEN 0 THEN 'System' WHEN 10 THEN 'Remote Interactive' WHEN 11 THEN 'Cached Interactive' WHEN 12 THEN 'Cached Remote Interactive' WHEN 13 THEN 'Cached Unlock' WHEN 2 THEN 'Interactive' WHEN 3 THEN 'Network' WHEN 4 THEN 'Batch' WHEN 5 THEN 'OS Service' WHEN 7 THEN 'Unlock' WHEN 8 THEN 'Network Cleartext' WHEN 9 THEN 'New Credentials' WHEN 99 THEN 'Other' END``` |
| logon_type_id | ```3::NUMBER``` |
| message | ```MESSAGE::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.logged_time | ```date_part('epoch_milliseconds', to_varchar(INGESTED_TIME::TIMESTAMP_LTZ, 'YYYY-MM-DD"T"HH24:MI:SS.FF3"Z"')::TIMESTAMP_LTZ)``` |
| metadata.logged_time_dt | ```to_varchar(INGESTED_TIME::TIMESTAMP_LTZ, 'YYYY-MM-DD"T"HH24:MI:SS.FF3"Z"')``` |
| metadata.product.name | ```'oracle-audit-logs'``` |
| metadata.product.vendor_name | ```'oracle'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```IP_ADDRESS::VARCHAR``` |
| status | ```CASE (CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '3%%' THEN 2 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '3%%' THEN 2 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', time::TIMESTAMP_LTZ)``` |
| time_dt | ```time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300201::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300201::NUMBER``` |
| user.credential_uid | ```CREDENTIALS::VARCHAR``` |
| user.domain | ```ADDITIONAL_DETAILS:domainName::VARCHAR``` |
| user.email_addr | ```ADDITIONAL_DETAILS:actorName::VARCHAR``` |
| user.name | ```ADDITIONAL_DETAILS:actorDisplayName::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
