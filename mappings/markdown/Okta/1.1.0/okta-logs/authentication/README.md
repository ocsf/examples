# Event Dossier: Okta Logs to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `okta`
* Product name: `okta-logs`
* Event codes: `EVENT_TYPE ILIKE '%user.authentication%' OR EVENT_TYPE ILIKE '%user.mfa.okta_verify%' OR EVENT_TYPE IN ('user.session.start' , 'system.push.send_factor_verify_push')`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```IFF(EVENT_TYPE = 'user.authentication.slo', 2, 1)::NUMBER``` |
| activity_name | ```CASE (IFF(EVENT_TYPE = 'user.authentication.slo', 2, 1)::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```ACTOR_ALTERNATE_ID::VARCHAR``` |
| actor.user.name | ```ACTOR_DISPLAY_NAME::VARCHAR``` |
| actor.user.type | ```CASE (CASE WHEN ACTOR_TYPE IS NULL THEN 0 WHEN ACTOR_TYPE = 'User' THEN 1 WHEN ACTOR_TYPE = 'SystemPrincipal' THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| actor.user.type_id | ```CASE WHEN ACTOR_TYPE IS NULL THEN 0 WHEN ACTOR_TYPE = 'User' THEN 1 WHEN ACTOR_TYPE = 'SystemPrincipal' THEN 3 ELSE 99 END::NUMBER``` |
| actor.user.uid | ```ACTOR_ID::VARCHAR``` |
| auth_protocol | ```CASE (CASE WHEN DEBUG_CONTEXT:debugData:signOnMode ILIKE '%OpenID%' THEN 4 WHEN DEBUG_CONTEXT:debugData:signOnMode ILIKE '%SAML%' THEN 5 WHEN EVENT_TYPE = 'user.authentication.auth_via_radius' THEN 10 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```CASE WHEN DEBUG_CONTEXT:debugData:signOnMode ILIKE '%OpenID%' THEN 4 WHEN DEBUG_CONTEXT:debugData:signOnMode ILIKE '%SAML%' THEN 5 WHEN EVENT_TYPE = 'user.authentication.auth_via_radius' THEN 10 ELSE 99 END::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| device.domain | ```SECURITY_CONTEXT:domain::VARCHAR``` |
| device.ip | ```CLIENT_IP_ADDRESS::VARCHAR``` |
| device.location.city | ```CLIENT_GEOGRAPHICAL_CONTEXT_CITY::VARCHAR``` |
| device.location.coordinates | ```ARRAY_CONSTRUCT(CLIENT_GEOGRAPHICAL_CONTEXT_GEOLOCATION:lon, CLIENT_GEOGRAPHICAL_CONTEXT_GEOLOCATION:lat)::ARRAY``` |
| device.location.country | ```CLIENT_GEOGRAPHICAL_CONTEXT_COUNTRY::VARCHAR``` |
| device.location.isp | ```SECURITY_CONTEXT:isp::VARCHAR``` |
| device.location.postal_code | ```CLIENT_GEOGRAPHICAL_CONTEXT_POSTAL_CODE::VARCHAR``` |
| device.org.name | ```SECURITY_CONTEXT:asOrg::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN CLIENT_USER_AGENT_OS ILIKE 'unknown' OR CLIENT_USER_AGENT_OS IS NULL THEN 0 WHEN CLIENT_USER_AGENT_OS ILIKE 'Windows%' THEN 100 WHEN CLIENT_USER_AGENT_OS IN ('Linux', 'Ubuntu') THEN 200 WHEN CLIENT_USER_AGENT_OS ILIKE 'Android%' THEN 201 WHEN CLIENT_USER_AGENT_OS ILIKE 'Mac%' THEN 300 WHEN CLIENT_USER_AGENT_OS ILIKE 'iOS%ipad%' THEN 302 WHEN CLIENT_USER_AGENT_OS ILIKE 'iOS%' THEN 301 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN CLIENT_USER_AGENT_OS ILIKE 'unknown' OR CLIENT_USER_AGENT_OS IS NULL THEN 0 WHEN CLIENT_USER_AGENT_OS ILIKE 'Windows%' THEN 100 WHEN CLIENT_USER_AGENT_OS IN ('Linux', 'Ubuntu') THEN 200 WHEN CLIENT_USER_AGENT_OS ILIKE 'Android%' THEN 201 WHEN CLIENT_USER_AGENT_OS ILIKE 'Mac%' THEN 300 WHEN CLIENT_USER_AGENT_OS ILIKE 'iOS%ipad%' THEN 302 WHEN CLIENT_USER_AGENT_OS ILIKE 'iOS%' THEN 301 ELSE 99 END::NUMBER``` |
| device.risk_level | ```CASE (CASE REGEXP_SUBSTR(DEBUG_CONTEXT:debugData:risk::VARCHAR, 'level=(\\w+)', 1, 1, 'e', 1) WHEN 'LOW' THEN 1 WHEN 'MEDIUM' THEN 2 WHEN 'HIGH' THEN 3 ELSE 0 END::NUMBER) WHEN 0 THEN 'Info' WHEN 1 THEN 'Low' WHEN 2 THEN 'Medium' WHEN 3 THEN 'High' WHEN 4 THEN 'Critical' END``` |
| device.risk_level_id | ```CASE REGEXP_SUBSTR(DEBUG_CONTEXT:debugData:risk::VARCHAR, 'level=(\\w+)', 1, 1, 'e', 1) WHEN 'LOW' THEN 1 WHEN 'MEDIUM' THEN 2 WHEN 'HIGH' THEN 3 ELSE 0 END::NUMBER``` |
| device.type | ```CASE (CASE WHEN CLIENT_DEVICE ILIKE 'unknown' OR CLIENT_DEVICE IS NULL THEN 0 WHEN CLIENT_DEVICE = 'Computer' THEN 2 WHEN CLIENT_DEVICE = 'Tablet' THEN 4 WHEN CLIENT_DEVICE = 'Mobile' THEN 5 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| device.type_id | ```CASE WHEN CLIENT_DEVICE ILIKE 'unknown' OR CLIENT_DEVICE IS NULL THEN 0 WHEN CLIENT_DEVICE = 'Computer' THEN 2 WHEN CLIENT_DEVICE = 'Tablet' THEN 4 WHEN CLIENT_DEVICE = 'Mobile' THEN 5 ELSE 99 END::NUMBER``` |
| device.uid | ```CLIENT_ID::VARCHAR``` |
| device.zone | ```CLIENT_ZONE::VARCHAR``` |
| http_request.uid | ```DEBUG_CONTEXT:debugData:requestId::VARCHAR``` |
| http_request.url.hostname | ```IFF(PARSE_URL(DEBUG_CONTEXT:debugData:origin, 1):error IS NULL, PARSE_URL(DEBUG_CONTEXT:debugData:origin, 1):host, NULL)::VARCHAR``` |
| http_request.url.path | ```SPLIT_PART(DEBUG_CONTEXT:debugData:url, '?', 1)::VARCHAR``` |
| http_request.url.port | ```IFF(PARSE_URL(DEBUG_CONTEXT:debugData:origin, 1):error IS NULL, PARSE_URL(DEBUG_CONTEXT:debugData:origin, 1):port, NULL)::VARCHAR``` |
| http_request.url.query_string | ```IFF(SPLIT_PART(DEBUG_CONTEXT:debugData:url, '?', -1) = '', NULL, SPLIT_PART(DEBUG_CONTEXT:debugData:url, '?', -1))::VARCHAR``` |
| http_request.url.scheme | ```IFF(PARSE_URL(DEBUG_CONTEXT:debugData:origin, 1):error IS NULL, PARSE_URL(DEBUG_CONTEXT:debugData:origin, 1):scheme, NULL)::VARCHAR``` |
| http_request.user_agent | ```CLIENT_USER_AGENT_RAW_USER_AGENT::VARCHAR``` |
| logon_process.uid | ```UUID::VARCHAR``` |
| message | ```DISPLAY_MESSAGE::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'okta-logs'``` |
| metadata.product.vendor_name | ```'okta'``` |
| metadata.version | ```'1.1.0'``` |
| session.uid | ```AUTHENTICATION_CONTEXT:externalSessionId::VARCHAR``` |
| severity | ```CASE (CASE WHEN SEVERITY IS NULL THEN 0 WHEN SEVERITY = 'INFO' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN SEVERITY IS NULL THEN 0 WHEN SEVERITY = 'INFO' THEN 1 ELSE 99 END::NUMBER``` |
| start_time | ```date_part('epoch_milliseconds', PUBLISHED::TIMESTAMP_LTZ)``` |
| start_time_dt | ```to_varchar(PUBLISHED::TIMESTAMP_LTZ, 'YYYY-MM-DD"T"HH24:MI:SS.FF3"Z"')``` |
| status | ```CASE (CASE WHEN OUTCOME_RESULT IS NULL THEN 0 WHEN OUTCOME_RESULT = 'SUCCESS' THEN 1 WHEN OUTCOME_RESULT = 'FAILURE' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_detail | ```OUTCOME_REASON::VARCHAR``` |
| status_id | ```CASE WHEN OUTCOME_RESULT IS NULL THEN 0 WHEN OUTCOME_RESULT = 'SUCCESS' THEN 1 WHEN OUTCOME_RESULT = 'FAILURE' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', published::TIMESTAMP_LTZ)``` |
| time_dt | ```to_varchar(published::TIMESTAMP_LTZ, 'YYYY-MM-DD"T"HH24:MI:SS.FF3"Z"')``` |
| type_name | ```CASE (CASE WHEN SEVERITY IS NULL THEN 300200 WHEN SEVERITY = 'INFO' THEN 300201 ELSE 300299 END::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```CASE WHEN SEVERITY IS NULL THEN 300200 WHEN SEVERITY = 'INFO' THEN 300201 ELSE 300299 END::NUMBER``` |
| user.email_addr | ```ACTOR_ALTERNATE_ID::VARCHAR``` |
| user.name | ```ACTOR_DISPLAY_NAME::VARCHAR``` |
| user.type | ```CASE (CASE WHEN ACTOR_TYPE IS NULL THEN 0 WHEN ACTOR_TYPE = 'User' THEN 1 WHEN ACTOR_TYPE = 'SystemPrincipal' THEN 3 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| user.type_id | ```CASE WHEN ACTOR_TYPE IS NULL THEN 0 WHEN ACTOR_TYPE = 'User' THEN 1 WHEN ACTOR_TYPE = 'SystemPrincipal' THEN 3 ELSE 99 END::NUMBER``` |
| user.uid | ```ACTOR_ID::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
