# Event Dossier: Gcp Audit to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `gcp`
* Product name: `gcp-audit`
* Event codes: `LOG_TYPE = 'requests'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE WHEN HTTP_REQUEST:requestMethod = 'CONNECT' THEN 1 WHEN HTTP_REQUEST:requestMethod = 'DELETE' THEN 2 WHEN HTTP_REQUEST:requestMethod = 'GET' THEN 3 WHEN HTTP_REQUEST:requestMethod = 'HEAD' THEN 4 WHEN HTTP_REQUEST:requestMethod = 'OPTIONS' THEN 5 WHEN HTTP_REQUEST:requestMethod = 'POST' THEN 6 WHEN HTTP_REQUEST:requestMethod = 'PUT' THEN 7 WHEN HTTP_REQUEST:requestMethod = 'TRACE' THEN 8 WHEN HTTP_REQUEST:requestMethod IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN HTTP_REQUEST:requestMethod = 'CONNECT' THEN 1 WHEN HTTP_REQUEST:requestMethod = 'DELETE' THEN 2 WHEN HTTP_REQUEST:requestMethod = 'GET' THEN 3 WHEN HTTP_REQUEST:requestMethod = 'HEAD' THEN 4 WHEN HTTP_REQUEST:requestMethod = 'OPTIONS' THEN 5 WHEN HTTP_REQUEST:requestMethod = 'POST' THEN 6 WHEN HTTP_REQUEST:requestMethod = 'PUT' THEN 7 WHEN HTTP_REQUEST:requestMethod = 'TRACE' THEN 8 WHEN HTTP_REQUEST:requestMethod IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| api.operation | ```OPERATION::VARCHAR``` |
| api.response.code | ```HTTP_REQUEST:status::NUMBER``` |
| api.response.error_message | ```CASE WHEN HTTP_REQUEST:status ILIKE '4%%' THEN RAW:textPayload ELSE NULL END::VARCHAR``` |
| api.service.labels | ```RAW:labels::VARCHAR``` |
| api.service.name | ```RESOURCE_LABELS:service_name::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| cloud.account.type | ```CASE (5::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'LDAP Account' WHEN 10 THEN 'AWS Account' WHEN 2 THEN 'Windows Account' WHEN 3 THEN 'AWS IAM User' WHEN 4 THEN 'AWS IAM Role' WHEN 5 THEN 'GCP Account' WHEN 6 THEN 'Azure AD Account' WHEN 7 THEN 'Mac OS Account' WHEN 8 THEN 'Apple Account' WHEN 9 THEN 'Linux Account' WHEN 99 THEN 'Other' END``` |
| cloud.account.type_id | ```5::NUMBER``` |
| cloud.account.uid | ```RAW:labels:instanceId::VARCHAR``` |
| cloud.project_uid | ```RESOURCE_LABELS:project_id::VARCHAR``` |
| cloud.provider | ```'GCP'::VARCHAR``` |
| cloud.region | ```RESOURCE_LABELS:location::VARCHAR``` |
| connection_info.boundary | ```CASE (5::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Localhost' WHEN 10 THEN 'Gateway VPC' WHEN 11 THEN 'Internet Gateway' WHEN 2 THEN 'Internal' WHEN 3 THEN 'External' WHEN 4 THEN 'Same VPC' WHEN 5 THEN 'Internet/VPC Gateway' WHEN 6 THEN 'Virtual Private Gateway' WHEN 7 THEN 'Intra-region VPC' WHEN 8 THEN 'Inter-region VPC' WHEN 9 THEN 'Local Gateway' WHEN 99 THEN 'Other' END``` |
| connection_info.boundary_id | ```5::NUMBER``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(HTTP_REQUEST:remoteIp::VARCHAR, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(HTTP_REQUEST:remoteIp::VARCHAR, 'INET'):family::NUMBER``` |
| dst_endpoint.ip | ```HTTP_REQUEST:serverIp::VARCHAR``` |
| http_request.http_method | ```CASE WHEN HTTP_REQUEST:requestMethod = 'CONNECT' THEN 'CONNECT' WHEN HTTP_REQUEST:requestMethod = 'DELETE' THEN 'DELETE' WHEN HTTP_REQUEST:requestMethod = 'GET' THEN 'GET' WHEN HTTP_REQUEST:requestMethod = 'HEAD' THEN 'HEAD' WHEN HTTP_REQUEST:requestMethod = 'OPTIONS' THEN 'OPTIONS' WHEN HTTP_REQUEST:requestMethod = 'POST' THEN 'POST' WHEN HTTP_REQUEST:requestMethod = 'PUT' THEN 'PUT' WHEN HTTP_REQUEST:requestMethod = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.length | ```HTTP_REQUEST:requestSize::NUMBER``` |
| http_request.referrer | ```HTTP_REQUEST:referer::VARCHAR``` |
| http_request.url.resource_type | ```RESOURCE_TYPE::VARCHAR``` |
| http_request.url.scheme | ```REGEXP_SUBSTR(HTTP_REQUEST:requestUrl, '^([a-zA-Z]+)')::VARCHAR``` |
| http_request.url.url_string | ```HTTP_REQUEST:requestUrl::VARCHAR``` |
| http_request.user_agent | ```HTTP_REQUEST:userAgent::VARCHAR``` |
| http_request.version | ```REGEXP_SUBSTR(HTTP_REQUEST:protocol, '([0-9\.]+)')::VARCHAR``` |
| http_response.code | ```HTTP_REQUEST:status::NUMBER``` |
| http_response.latency | ```REGEXP_SUBSTR(HTTP_REQUEST:latency, '([0-9\.]+)')::NUMBER``` |
| http_response.length | ```HTTP_REQUEST:responseSize::NUMBER``` |
| http_status | ```HTTP_REQUEST:status::NUMBER``` |
| message | ```RAW:textPayload::VARCHAR``` |
| metadata.labels | ```LOG_LABELS::VARCHAR``` |
| metadata.log_name | ```LOG_NAME::VARCHAR``` |
| metadata.logged_time | ```date_part('epoch_milliseconds', RAW:receiveTimestamp::TIMESTAMP_LTZ)``` |
| metadata.logged_time_dt | ```RAW:receiveTimestamp::TIMESTAMP_LTZ``` |
| metadata.product.name | ```'gcp-audit'``` |
| metadata.product.vendor_name | ```'gcp'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN SEVERITY='INFO' THEN 1 WHEN SEVERITY='WARNING' THEN 2 WHEN SEVERITY='ERROR' THEN 4 WHEN SEVERITY IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN SEVERITY='INFO' THEN 1 WHEN SEVERITY='WARNING' THEN 2 WHEN SEVERITY='ERROR' THEN 4 WHEN SEVERITY IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| src_endpoint.ip | ```HTTP_REQUEST:remoteIp::VARCHAR``` |
| status | ```CASE (CASE WHEN HTTP_REQUEST:status ILIKE '2%%' THEN 1 WHEN HTTP_REQUEST:status ILIKE '4%%' THEN 2 WHEN HTTP_REQUEST:status IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_detail | ```RAW:textPayload::VARCHAR``` |
| status_id | ```CASE WHEN HTTP_REQUEST:status ILIKE '2%%' THEN 1 WHEN HTTP_REQUEST:status ILIKE '4%%' THEN 2 WHEN HTTP_REQUEST:status IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN HTTP_REQUEST:requestMethod = 'CONNECT' THEN 400201 WHEN HTTP_REQUEST:requestMethod = 'DELETE' THEN 400202 WHEN HTTP_REQUEST:requestMethod = 'GET' THEN 400203 WHEN HTTP_REQUEST:requestMethod = 'HEAD' THEN 400204 WHEN HTTP_REQUEST:requestMethod = 'OPTIONS' THEN 400205 WHEN HTTP_REQUEST:requestMethod = 'POST' THEN 400206 WHEN HTTP_REQUEST:requestMethod = 'PUT' THEN 400207 WHEN HTTP_REQUEST:requestMethod = 'TRACE' THEN 400208 WHEN HTTP_REQUEST:requestMethod IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN HTTP_REQUEST:requestMethod = 'CONNECT' THEN 400201 WHEN HTTP_REQUEST:requestMethod = 'DELETE' THEN 400202 WHEN HTTP_REQUEST:requestMethod = 'GET' THEN 400203 WHEN HTTP_REQUEST:requestMethod = 'HEAD' THEN 400204 WHEN HTTP_REQUEST:requestMethod = 'OPTIONS' THEN 400205 WHEN HTTP_REQUEST:requestMethod = 'POST' THEN 400206 WHEN HTTP_REQUEST:requestMethod = 'PUT' THEN 400207 WHEN HTTP_REQUEST:requestMethod = 'TRACE' THEN 400208 WHEN HTTP_REQUEST:requestMethod IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
