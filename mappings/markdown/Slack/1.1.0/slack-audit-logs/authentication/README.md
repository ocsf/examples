# Event Dossier: Slack Audit Logs to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `slack`
* Product name: `slack-audit-logs`
* Event codes: `ACTION IN ('user_login', 'user_login_failed')`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```CASE WHEN ACTION = 'user_login' THEN 1 WHEN ACTION = 'user_login_failed' THEN 2 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN ACTION = 'user_login' THEN 1 WHEN ACTION = 'user_login_failed' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```ACTOR_USER_EMAIL::VARCHAR``` |
| actor.user.name | ```ACTOR_USER_NAME::VARCHAR``` |
| actor.user.type | ```CASE (CASE WHEN ACTOR_TYPE IS NULL THEN 0 WHEN ACTOR_TYPE = 'user' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| actor.user.type_id | ```CASE WHEN ACTOR_TYPE IS NULL THEN 0 WHEN ACTOR_TYPE = 'user' THEN 1 ELSE 99 END::NUMBER``` |
| actor.user.uid | ```ACTOR_USER_ID::VARCHAR``` |
| auth_protocol | ```CASE (CASE WHEN DETAILS:config_type IS NULL THEN 0 WHEN DETAILS:config_type = 'SAML' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```CASE WHEN DETAILS:config_type IS NULL THEN 0 WHEN DETAILS:config_type = 'SAML' THEN 5 ELSE 99 END::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| dst_endpoint.uid | ```CONTEXT_LOCATION_ID::VARCHAR``` |
| http_request.user_agent | ```CONTEXT_USER_AGENT::VARCHAR``` |
| is_mfa | ```CASE WHEN DETAILS:config_type IS NOT NULL THEN TRUE ELSE FALSE END::BOOLEAN``` |
| logon_process.file.name | ```ENTITY_FILE_NAME::VARCHAR``` |
| logon_process.file.uid | ```ENTITY_FILE_ID::VARCHAR``` |
| logon_process.session.uid | ```CONTEXT_SESSION_ID::VARCHAR``` |
| logon_process.user.domain | ```CONTEXT_LOCATION_DOMAIN::VARCHAR``` |
| metadata.product.name | ```'slack-audit-logs'``` |
| metadata.product.vendor_name | ```'slack'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```CONTEXT_IP_ADDRESS::VARCHAR``` |
| status | ```CASE (CASE WHEN ACTION = 'user_login' THEN 1 WHEN ACTION = 'user_login_failed' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN ACTION = 'user_login' THEN 1 WHEN ACTION = 'user_login_failed' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', date_create::TIMESTAMP_LTZ)``` |
| time_dt | ```date_create::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((300200 + (CASE WHEN ACTION = 'user_login' THEN 1 WHEN ACTION = 'user_login_failed' THEN 2 ELSE 99 END))::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```(300200 + (CASE WHEN ACTION = 'user_login' THEN 1 WHEN ACTION = 'user_login_failed' THEN 2 ELSE 99 END))::NUMBER``` |
| user.email_addr | ```RAW:entity:user:email::VARCHAR``` |
| user.name | ```RAW:entity:user:name::VARCHAR``` |
| user.type | ```CASE (CASE WHEN ENTITY_TYPE IS NULL THEN 0 WHEN ENTITY_TYPE = 'user' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| user.type_id | ```CASE WHEN ENTITY_TYPE IS NULL THEN 0 WHEN ENTITY_TYPE = 'user' THEN 1 ELSE 99 END::NUMBER``` |
| user.uid | ```RAW:entity:user:id::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
