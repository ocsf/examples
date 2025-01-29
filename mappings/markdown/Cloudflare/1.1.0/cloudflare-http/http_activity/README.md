# Event Dossier: Cloudflare Http to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `cloudflare`
* Product name: `cloudflare-http`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN WAF_ACTION = 'unknown' THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN WAF_ACTION = 'unknown' THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```DECODE(CLIENT_REQUEST_METHOD, 'CONNECT', 1, 'DELETE', 2, 'GET', 3, 'HEAD', 4, 'OPTIONS', 5, 'POST', 6, 'PUT', 7, 'TRACE', 8,0)``` |
| activity_name | ```CASE (DECODE(CLIENT_REQUEST_METHOD, 'CONNECT', 1, 'DELETE', 2, 'GET', 3, 'HEAD', 4, 'OPTIONS', 5, 'POST', 6, 'PUT', 7, 'TRACE', 8,0)) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.boundary | ```CASE (5::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Localhost' WHEN 10 THEN 'Gateway VPC' WHEN 11 THEN 'Internet Gateway' WHEN 2 THEN 'Internal' WHEN 3 THEN 'External' WHEN 4 THEN 'Same VPC' WHEN 5 THEN 'Internet/VPC Gateway' WHEN 6 THEN 'Virtual Private Gateway' WHEN 7 THEN 'Intra-region VPC' WHEN 8 THEN 'Inter-region VPC' WHEN 9 THEN 'Local Gateway' WHEN 99 THEN 'Other' END``` |
| connection_info.boundary_id | ```5::NUMBER``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(ORIGIN_IP, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(ORIGIN_IP, 'INET'):family::NUMBER``` |
| connection_info.uid | ```HASH::VARCHAR``` |
| dst_endpoint.hostname | ```CLIENT_REQUEST_HOST::VARCHAR``` |
| dst_endpoint.ip | ```COALESCE(ORIGIN_IP, EDGE_SERVER_IP)::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', EDGE_END_TIMESTAMP::TIMESTAMP_LTZ)``` |
| end_time_dt | ```EDGE_END_TIMESTAMP::TIMESTAMP_LTZ``` |
| firewall_rule.name | ```parse_json(FIREWALL_MATCHES_RULE_I_DS)[0]::VARCHAR``` |
| http_request.http_method | ```CLIENT_REQUEST_METHOD::VARCHAR``` |
| http_request.referrer | ```CLIENT_REQUEST_REFERER::VARCHAR``` |
| http_request.url.hostname | ```CLIENT_REQUEST_HOST::VARCHAR``` |
| http_request.url.path | ```CLIENT_REQUEST_PATH::VARCHAR``` |
| http_request.url.port | ```CLIENT_SRC_PORT::VARCHAR``` |
| http_request.user_agent | ```CLIENT_REQUEST_USER_AGENT::VARCHAR``` |
| http_response.length | ```COALESCE(EDGE_RESPONSE_BYTES, ORIGIN_RESPONSE_BYTES)::NUMBER``` |
| http_response.status | ```COALESCE(EDGE_RESPONSE_STATUS, ORIGIN_RESPONSE_STATUS)::VARCHAR``` |
| metadata.product.name | ```'cloudflare-http'``` |
| metadata.product.vendor_name | ```'cloudflare'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| src_endpoint.location.country | ```CLIENT_COUNTRY::VARCHAR``` |
| src_endpoint.port | ```CLIENT_SRC_PORT::VARCHAR``` |
| src_endpoint.type | ```CASE (CASE WHEN CLIENT_DEVICE_TYPE = 'desktop' THEN 2 WHEN CLIENT_DEVICE_TYPE = 'mobile' THEN 5 WHEN CLIENT_DEVICE_TYPE = 'tablet' THEN 4 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| src_endpoint.type_id | ```CASE WHEN CLIENT_DEVICE_TYPE = 'desktop' THEN 2 WHEN CLIENT_DEVICE_TYPE = 'mobile' THEN 5 WHEN CLIENT_DEVICE_TYPE = 'tablet' THEN 4 ELSE 99 END::NUMBER``` |
| start_time | ```date_part('epoch_milliseconds', EDGE_START_TIMESTAMP::TIMESTAMP_LTZ)``` |
| start_time_dt | ```EDGE_START_TIMESTAMP::TIMESTAMP_LTZ``` |
| status_code | ```CACHE_RESPONSE_STATUS::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', edge_start_timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```edge_start_timestamp::TIMESTAMP_LTZ``` |
| type_name | ```CASE (DECODE(CLIENT_REQUEST_METHOD, 'CONNECT', 400201, 'DELETE', 400202, 'GET', 400203, 'HEAD', 400204, 'OPTIONS', 400205, 'POST', 400206, 'PUT', 400207, 'TRACE', 400208,400200)) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```DECODE(CLIENT_REQUEST_METHOD, 'CONNECT', 400201, 'DELETE', 400202, 'GET', 400203, 'HEAD', 400204, 'OPTIONS', 400205, 'POST', 400206, 'PUT', 400207, 'TRACE', 400208,400200)``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
