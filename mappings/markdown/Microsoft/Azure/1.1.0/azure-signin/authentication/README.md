# Event Dossier: Azure Signin to OCSF class Authentication

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `authentication`
* Vendor name: `azure`
* Product name: `azure-signin`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| activity_id | ```1::NUMBER``` |
| activity_name | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Logon' WHEN 2 THEN 'Logoff' WHEN 3 THEN 'Authentication Ticket' WHEN 4 THEN 'Service Ticket Request' WHEN 5 THEN 'Service Ticket Renew' WHEN 99 THEN 'Other' END``` |
| api.version | ```OPERATION_VERSION::VARCHAR``` |
| auth_protocol | ```CASE (CASE WHEN PROPERTIES:authenticationProtocol='NTLM' THEN 1 WHEN PROPERTIES:authenticationProtocol='Kerberos' THEN 2 WHEN PROPERTIES:authenticationProtocol='Digest' THEN 3 WHEN PROPERTIES:authenticationProtocol='OpenID' THEN 4 WHEN PROPERTIES:authenticationProtocol='SAML' THEN 5 WHEN PROPERTIES:authenticationProtocol='OAUTH 2.0' THEN 6 WHEN PROPERTIES:authenticationProtocol='PAP' THEN 7 WHEN PROPERTIES:authenticationProtocol='CHAP' THEN 8 WHEN PROPERTIES:authenticationProtocol='EAP' THEN 9 WHEN PROPERTIES:authenticationProtocol='RADIUS' THEN 10 WHEN PROPERTIES:authenticationProtocol IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'NTLM' WHEN 10 THEN 'RADIUS' WHEN 2 THEN 'Kerberos' WHEN 3 THEN 'Digest' WHEN 4 THEN 'OpenID' WHEN 5 THEN 'SAML' WHEN 6 THEN 'OAUTH 2.0' WHEN 7 THEN 'PAP' WHEN 8 THEN 'CHAP' WHEN 9 THEN 'EAP' WHEN 99 THEN 'Other' END``` |
| auth_protocol_id | ```CASE WHEN PROPERTIES:authenticationProtocol='NTLM' THEN 1 WHEN PROPERTIES:authenticationProtocol='Kerberos' THEN 2 WHEN PROPERTIES:authenticationProtocol='Digest' THEN 3 WHEN PROPERTIES:authenticationProtocol='OpenID' THEN 4 WHEN PROPERTIES:authenticationProtocol='SAML' THEN 5 WHEN PROPERTIES:authenticationProtocol='OAUTH 2.0' THEN 6 WHEN PROPERTIES:authenticationProtocol='PAP' THEN 7 WHEN PROPERTIES:authenticationProtocol='CHAP' THEN 8 WHEN PROPERTIES:authenticationProtocol='EAP' THEN 9 WHEN PROPERTIES:authenticationProtocol='RADIUS' THEN 10 WHEN PROPERTIES:authenticationProtocol IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| category_name | ```CASE (3::NUMBER) WHEN 3 THEN 'Identity & Access Management' END``` |
| category_uid | ```3::NUMBER``` |
| class_name | ```'authentication'``` |
| class_uid | ```3002``` |
| cloud.account.name | ```PROPERTIES:homeTenantName::VARCHAR``` |
| cloud.account.type | ```CASE (6::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'LDAP Account' WHEN 10 THEN 'AWS Account' WHEN 2 THEN 'Windows Account' WHEN 3 THEN 'AWS IAM User' WHEN 4 THEN 'AWS IAM Role' WHEN 5 THEN 'GCP Account' WHEN 6 THEN 'Azure AD Account' WHEN 7 THEN 'Mac OS Account' WHEN 8 THEN 'Apple Account' WHEN 9 THEN 'Linux Account' WHEN 99 THEN 'Other' END``` |
| cloud.account.type_id | ```6::NUMBER``` |
| cloud.account.uid | ```TENANT_ID::VARCHAR``` |
| cloud.provider | ```PROPERTIES_TOKEN_ISSUER_TYPE::VARCHAR``` |
| device.is_managed | ```PROPERTIES_DEVICE_DETAIL:isManaged::BOOLEAN``` |
| device.name | ```PROPERTIES_DEVICE_DETAIL:displayName::VARCHAR``` |
| device.os.name | ```PROPERTIES_DEVICE_DETAIL:operatingSystem::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='WindowsPhone' THEN 101 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem ilike '%Windows%' THEN 100 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='Linux' THEN 200 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='Android' THEN 201 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='MacOs' THEN 300 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem ilike 'iOS' THEN 301 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='iPadOS' THEN 302 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='Solaris' THEN 400 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='AIX' THEN 401 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='HP-UX' THEN 402 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='WindowsPhone' THEN 101 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem ilike '%Windows%' THEN 100 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='Linux' THEN 200 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='Android' THEN 201 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='MacOs' THEN 300 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem ilike 'iOS' THEN 301 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='iPadOS' THEN 302 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='Solaris' THEN 400 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='AIX' THEN 401 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem='HP-UX' THEN 402 WHEN PROPERTIES_DEVICE_DETAIL:operatingSystem IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| device.uid | ```PROPERTIES_DEVICE_DETAIL:deviceId::VARCHAR``` |
| http_request.uid | ```PROPERTIES:originalRequestId::VARCHAR``` |
| http_request.user_agent | ```PROPERTIES:userAgent::VARCHAR``` |
| is_mfa | ```IFF(PROPERTIES:authenticationRequirement='multiFactorAuthentication', true, false)::BOOLEAN``` |
| logon_process.created_time | ```date_part('epoch_milliseconds', PROPERTIES_CREATED_DATE_TIME::TIMESTAMP_LTZ)``` |
| logon_process.created_time_dt | ```PROPERTIES_CREATED_DATE_TIME::TIMESTAMP_LTZ``` |
| metadata.event_code | ```category``` |
| metadata.product.name | ```'azure-signin'``` |
| metadata.product.vendor_name | ```'azure'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN PROPERTIES_RISK_LEVEL_AGGREGATED='informational' THEN 1 WHEN COALESCE(PROPERTIES_RISK_LEVEL_AGGREGATED, PROPERTIES:riskLevel)='low' THEN 2 WHEN COALESCE(PROPERTIES_RISK_LEVEL_AGGREGATED, PROPERTIES:riskLevel)='medium' THEN 3 WHEN COALESCE(PROPERTIES_RISK_LEVEL_AGGREGATED, PROPERTIES:riskLevel)='high' THEN 4 WHEN PROPERTIES_RISK_LEVEL_AGGREGATED='critical' THEN 5 WHEN PROPERTIES_RISK_LEVEL_AGGREGATED='fatal' THEN 6 WHEN PROPERTIES_RISK_LEVEL_AGGREGATED IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN PROPERTIES_RISK_LEVEL_AGGREGATED='informational' THEN 1 WHEN COALESCE(PROPERTIES_RISK_LEVEL_AGGREGATED, PROPERTIES:riskLevel)='low' THEN 2 WHEN COALESCE(PROPERTIES_RISK_LEVEL_AGGREGATED, PROPERTIES:riskLevel)='medium' THEN 3 WHEN COALESCE(PROPERTIES_RISK_LEVEL_AGGREGATED, PROPERTIES:riskLevel)='high' THEN 4 WHEN PROPERTIES_RISK_LEVEL_AGGREGATED='critical' THEN 5 WHEN PROPERTIES_RISK_LEVEL_AGGREGATED='fatal' THEN 6 WHEN PROPERTIES_RISK_LEVEL_AGGREGATED IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| src_endpoint.ip | ```CALLER_IP_ADDRESS::VARCHAR``` |
| src_endpoint.location.city | ```PROPERTIES_LOCATION:city::VARCHAR``` |
| src_endpoint.location.country | ```PROPERTIES_LOCATION:countryOrRegion::VARCHAR``` |
| status | ```CASE (CASE WHEN PROPERTIES:statusCode='OK' THEN 1 WHEN PROPERTIES:statusCode IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_code | ```PROPERTIES_STATUS:errorCode::VARCHAR``` |
| status_detail | ```COALESCE(PROPERTIES_STATUS:failureReason, PROPERTIES_STATUS:additionalDetails)::VARCHAR``` |
| status_id | ```CASE WHEN PROPERTIES:statusCode='OK' THEN 1 WHEN PROPERTIES:statusCode IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (300201::NUMBER) WHEN 300200 THEN 'Authentication: Unknown' WHEN 300201 THEN 'Authentication: Logon' WHEN 300202 THEN 'Authentication: Logoff' WHEN 300203 THEN 'Authentication: Authentication Ticket' WHEN 300204 THEN 'Authentication: Service Ticket Request' WHEN 300205 THEN 'Authentication: Service Ticket Renew' WHEN 300299 THEN 'Authentication: Other' END``` |
| type_uid | ```300201::NUMBER``` |
| user.credential_uid | ```PROPERTIES:servicePrincipalCredentialKeyId::VARCHAR``` |
| user.name | ```COALESCE(PROPERTIES:userDisplayName, PROPERTIES:servicePrincipalName)::VARCHAR``` |
| user.type | ```CASE (CASE WHEN PROPERTIES:userType IN ('Member', 'User') THEN 1 WHEN PROPERTIES:userType='Admin' THEN 2 WHEN PROPERTIES:userType='System' THEN 3 WHEN PROPERTIES:userType IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'User' WHEN 2 THEN 'Admin' WHEN 3 THEN 'System' WHEN 99 THEN 'Other' END``` |
| user.type_id | ```CASE WHEN PROPERTIES:userType IN ('Member', 'User') THEN 1 WHEN PROPERTIES:userType='Admin' THEN 2 WHEN PROPERTIES:userType='System' THEN 3 WHEN PROPERTIES:userType IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| user.uid | ```COALESCE(PROPERTIES:userId, PROPERTIES:servicePrincipalId)::VARCHAR``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
