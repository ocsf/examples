# Event Dossier: Aws Cloudtrail to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `aws`
* Product name: `aws-cloudtrail`
* Event codes: `EVENT_NAME in ('ConsoleLogin', 'AssumeRoleWithSAML')`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.authorizations | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT_KEEP_NULL('decision', CASE WHEN EVENT_NAME = 'ConsoleLogin' THEN CASE WHEN RESPONSE_ELEMENTS:ConsoleLogin = 'Success' THEN 'allowed' ELSE 'denied' END WHEN EVENT_NAME = 'AssumeRoleWithSAML' THEN   CASE   WHEN RESPONSE_ELEMENTS:credentials:accessKeyId IS NOT NULL THEN 'allowed' ELSE 'denied' END END))``` |
| actor.session.credential_uid | ```USER_IDENTITY_ACCESS_KEY_ID::VARCHAR``` |
| actor.session.is_mfa | ```CASE WHEN ADDITIONAL_EVENT_DATA:MFAUsed = 'No' THEN FALSE WHEN ADDITIONAL_EVENT_DATA:MFAUsed = 'Yes' THEN TRUE  ELSE NULL::BOOLEAN END``` |
| actor.user.account.uid | ```RECIPIENT_ACCOUNT_ID::VARCHAR``` |
| actor.user.credential_uid | ```USER_IDENTITY_ACCESS_KEY_ID::VARCHAR``` |
| actor.user.email_addr | ```CASE WHEN EVENT_NAME = 'ConsoleLogin' and CONTAINS(USER_IDENTITY:arn, '/') THEN              SPLIT_PART(USER_IDENTITY:arn, '/', -1)   WHEN EVENT_NAME = 'AssumeRoleWithSAML' THEN REQUEST_PARAMETERS:roleSessionName::VARCHAR END``` |
| actor.user.name | ```CASE EVENT_NAME WHEN 'ConsoleLogin' THEN USER_IDENTITY_SESSION_CONTEXT_SESSION_ISSUER_USER_NAME::VARCHAR   ELSE USER_IDENTITY_USER_NAME::VARCHAR END``` |
| actor.user.org.uid | ```RECIPIENT_ACCOUNT_ID::VARCHAR``` |
| actor.user.uid | ```CASE EVENT_NAME WHEN 'ConsoleLogin' THEN USER_IDENTITY_ARN::VARCHAR   ELSE RESOURCES[0]:ARN::VARCHAR END``` |
| api.response.code | ```ERROR_CODE::NUMBER``` |
| api.response.error | ```ERROR_CODE::VARCHAR``` |
| api.response.error_message | ```ERROR_MESSAGE::VARCHAR``` |
| api.service.name | ```EVENT_SOURCE::VARCHAR``` |
| api.service.uid | ```EVENT_SOURCE::VARCHAR``` |
| api.service.version | ```EVENT_VERSION::VARCHAR``` |
| api.version | ```EVENT_VERSION::VARCHAR``` |
| auth_protocol | ```CASE (CASE WHEN EVENT_NAME = 'ConsoleLogin' THEN '99'::NUMBER WHEN EVENT_NAME = 'AssumeRoleWithSAML' THEN '5'::NUMBER END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```CASE WHEN EVENT_NAME = 'ConsoleLogin' THEN '99'::NUMBER WHEN EVENT_NAME = 'AssumeRoleWithSAML' THEN '5'::NUMBER END``` |
| category_name | ```CASE ('3'::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```'3'::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| cloud.account.uid | ```RECIPIENT_ACCOUNT_ID::VARCHAR``` |
| cloud.org.uid | ```RECIPIENT_ACCOUNT_ID::VARCHAR``` |
| cloud.provider | ```'AWS'::VARCHAR``` |
| cloud.region | ```AWS_REGION::VARCHAR``` |
| dst_endpoint.domain | ```'amazonaws.com'::VARCHAR``` |
| dst_endpoint.hostname | ```EVENT_SOURCE::VARCHAR``` |
| dst_endpoint.name | ```EVENT_SOURCE::VARCHAR``` |
| dst_endpoint.type | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| dst_endpoint.type_id | ```1::NUMBER``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| is_mfa | ```CASE  WHEN ADDITIONAL_EVENT_DATA:MFAUsed = 'No' THEN FALSE  WHEN ADDITIONAL_EVENT_DATA:MFAUsed = 'Yes' THEN TRUE  ELSE NULL::BOOLEAN END``` |
| is_remote | ```TRUE::BOOLEAN``` |
| metadata.event_code | ```event_name``` |
| metadata.product.name | ```'aws-cloudtrail'``` |
| metadata.product.vendor_name | ```'aws'``` |
| metadata.version | ```'1.1.0'``` |
| service.name | ```EVENT_SOURCE::VARCHAR``` |
| service.uid | ```EVENT_SOURCE::VARCHAR``` |
| service.version | ```EVENT_VERSION::VARCHAR``` |
| session.created_time | ```date_part('epoch_milliseconds', USER_IDENTITY_SESSION_CONTEXT_ATTRIBUTES_CREATION_DATE::TIMESTAMP_LTZ)``` |
| session.created_time_dt | ```USER_IDENTITY_SESSION_CONTEXT_ATTRIBUTES_CREATION_DATE::TIMESTAMP_LTZ``` |
| session.credential_uid | ```USER_IDENTITY_ACCESS_KEY_ID::VARCHAR``` |
| session.is_mfa | ```CASE  WHEN ADDITIONAL_EVENT_DATA:MFAUsed = 'No' THEN FALSE  WHEN ADDITIONAL_EVENT_DATA:MFAUsed = 'Yes' THEN TRUE  ELSE NULL::BOOLEAN END``` |
| session.issuer | ```USER_IDENTITY_SESSION_CONTEXT_SESSION_ISSUER_ARN::VARCHAR``` |
| src_endpoint.ip | ```SOURCE_IP_ADDRESS::VARCHAR``` |
| status | ```CASE (CASE WHEN EVENT_NAME = 'ConsoleLogin' THEN CASE WHEN RESPONSE_ELEMENTS:ConsoleLogin = '1'::NUMBER THEN '1'::number ELSE '2'::number END WHEN EVENT_NAME = 'AssumeRoleWithSAML' THEN CASE WHEN RESPONSE_ELEMENTS:credentials:accessKeyId IS NOT NULL THEN '1'::number ELSE '2'::number END END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_code | ```ERROR_CODE::VARCHAR``` |
| status_detail | ```ERROR_MESSAGE::VARCHAR``` |
| status_id | ```CASE WHEN EVENT_NAME = 'ConsoleLogin' THEN CASE WHEN RESPONSE_ELEMENTS:ConsoleLogin = '1'::NUMBER THEN '1'::number ELSE '2'::number END WHEN EVENT_NAME = 'AssumeRoleWithSAML' THEN CASE WHEN RESPONSE_ELEMENTS:credentials:accessKeyId IS NOT NULL THEN '1'::number ELSE '2'::number END END``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300201::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300201::NUMBER``` |
| user.account.uid | ```RECIPIENT_ACCOUNT_ID::VARCHAR``` |
| user.credential_uid | ```USER_IDENTITY_ACCESS_KEY_ID::VARCHAR``` |
| user.email_addr | ```CASE WHEN EVENT_NAME = 'ConsoleLogin' and CONTAINS(USER_IDENTITY:arn, '/') THEN              SPLIT_PART(USER_IDENTITY:arn, '/', -1) WHEN EVENT_NAME = 'AssumeRoleWithSAML' THEN REQUEST_PARAMETERS:roleSessionName::VARCHAR END``` |
| user.name | ```CASE EVENT_NAME WHEN 'ConsoleLogin' THEN USER_IDENTITY_SESSION_CONTEXT_SESSION_ISSUER_USER_NAME::VARCHAR   ELSE USER_IDENTITY_USER_NAME::VARCHAR END``` |
| user.org.uid | ```RECIPIENT_ACCOUNT_ID::VARCHAR``` |
| user.type | ```CASE (case when USER_IDENTITY_TYPE = 'Unknown' then 0 when USER_IDENTITY_TYPE in ('IAMUser', 'SAMLUser', 'WebIdentityUser') then 1 when USER_IDENTITY_TYPE = 'Root' then 2 else 99 end) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| user.type_id | ```case when USER_IDENTITY_TYPE = 'Unknown' then 0 when USER_IDENTITY_TYPE in ('IAMUser', 'SAMLUser', 'WebIdentityUser') then 1 when USER_IDENTITY_TYPE = 'Root' then 2 else 99 end``` |
| user.uid | ```CASE EVENT_NAME WHEN 'ConsoleLogin' THEN USER_IDENTITY_ARN::VARCHAR ELSE RESOURCES[0]:ARN::VARCHAR END``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
