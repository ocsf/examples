# Event Dossier: Aws Waf to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `aws`
* Product name: `aws-waf`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION = 'ALLOW' THEN 1 WHEN ACTION = 'BLOCK' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION = 'ALLOW' THEN 1 WHEN ACTION = 'BLOCK' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE   WHEN HTTP_REQUEST_HTTP_METHOD = 'CONNECT' THEN 1   WHEN HTTP_REQUEST_HTTP_METHOD = 'DELETE' THEN 2   WHEN HTTP_REQUEST_HTTP_METHOD = 'GET' THEN 3   WHEN HTTP_REQUEST_HTTP_METHOD = 'HEAD' THEN 4   WHEN HTTP_REQUEST_HTTP_METHOD = 'OPTIONS' THEN 5   WHEN HTTP_REQUEST_HTTP_METHOD = 'POST' THEN 6   WHEN HTTP_REQUEST_HTTP_METHOD = 'PUT' THEN 7   WHEN HTTP_REQUEST_HTTP_METHOD = 'TRACE' THEN 8 WHEN HTTP_REQUEST_HTTP_METHOD = NULL THEN 0   ELSE 99  END::NUMBER``` |
| activity_name | ```CASE (CASE   WHEN HTTP_REQUEST_HTTP_METHOD = 'CONNECT' THEN 1   WHEN HTTP_REQUEST_HTTP_METHOD = 'DELETE' THEN 2   WHEN HTTP_REQUEST_HTTP_METHOD = 'GET' THEN 3   WHEN HTTP_REQUEST_HTTP_METHOD = 'HEAD' THEN 4   WHEN HTTP_REQUEST_HTTP_METHOD = 'OPTIONS' THEN 5   WHEN HTTP_REQUEST_HTTP_METHOD = 'POST' THEN 6   WHEN HTTP_REQUEST_HTTP_METHOD = 'PUT' THEN 7   WHEN HTTP_REQUEST_HTTP_METHOD = 'TRACE' THEN 8 WHEN HTTP_REQUEST_HTTP_METHOD = NULL THEN 0   ELSE 99  END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| cloud.provider | ```'AWS'::VARCHAR``` |
| connection_info.boundary | ```CASE (5::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Localhost' WHEN 10 THEN 'Gateway VPC' WHEN 11 THEN 'Internet Gateway' WHEN 2 THEN 'Internal' WHEN 3 THEN 'External' WHEN 4 THEN 'Same VPC' WHEN 5 THEN 'Internet/VPC Gateway' WHEN 6 THEN 'Virtual Private Gateway' WHEN 7 THEN 'Intra-region VPC' WHEN 8 THEN 'Inter-region VPC' WHEN 9 THEN 'Local Gateway' WHEN 99 THEN 'Other' END``` |
| connection_info.boundary_id | ```5::NUMBER``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(HTTP_REQUEST_CLIENT_IP, 'INET'):family::NUMBER::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(HTTP_REQUEST_CLIENT_IP, 'INET'):family::NUMBER::NUMBER``` |
| connection_info.uid | ```HTTP_REQUEST_REQUEST_ID::VARCHAR``` |
| dst_endpoint.hostname | ```HTTP_REQUEST_HEADERS:host::VARCHAR``` |
| firewall_rule.match_details | ```TERMINATING_RULE_MATCH_DETAILS::VARCHAR``` |
| firewall_rule.rate_limit | ```RATE_BASED_RULE_LIST[0]:maxRateAllowed::NUMBER``` |
| firewall_rule.type | ```TERMINATING_RULE_TYPE::VARCHAR``` |
| firewall_rule.uid | ```TERMINATING_RULE_ID::VARCHAR``` |
| http_cookies.value | ```HTTP_REQUEST_HEADERS:cookie::VARCHAR``` |
| http_request.args | ```HTTP_REQUEST_ARGS::VARCHAR``` |
| http_request.http_method | ```CASE   WHEN HTTP_REQUEST_HTTP_METHOD = 'CONNECT' THEN 'CONNECT'   WHEN HTTP_REQUEST_HTTP_METHOD = 'DELETE' THEN 'DELETE'   WHEN HTTP_REQUEST_HTTP_METHOD = 'GET' THEN 'GET'   WHEN HTTP_REQUEST_HTTP_METHOD = 'HEAD' THEN 'HEAD'   WHEN HTTP_REQUEST_HTTP_METHOD = 'OPTIONS' THEN 'OPTIONS'   WHEN HTTP_REQUEST_HTTP_METHOD = 'POST' THEN 'POST'   WHEN HTTP_REQUEST_HTTP_METHOD = 'PUT' THEN 'PUT'   WHEN HTTP_REQUEST_HTTP_METHOD = 'TRACE' THEN 'TRACE'   ELSE NULL  END::VARCHAR``` |
| http_request.referrer | ```HTTP_REQUEST_HEADERS:referer::VARCHAR``` |
| http_request.uid | ```HTTP_REQUEST_REQUEST_ID::VARCHAR``` |
| http_request.url.hostname | ```HTTP_REQUEST_HEADERS:host::VARCHAR``` |
| http_request.url.path | ```HTTP_REQUEST_URI::VARCHAR``` |
| http_request.url.query_string | ```HTTP_REQUEST_ARGS::VARCHAR``` |
| http_request.user_agent | ```HTTP_REQUEST_HEADERS:"user-agent"::VARCHAR``` |
| http_request.version | ```HTTP_REQUEST_HTTP_VERSION::VARCHAR``` |
| metadata.product.name | ```'aws-waf'``` |
| metadata.product.vendor_name | ```'aws'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```HTTP_REQUEST_CLIENT_IP::VARCHAR``` |
| src_endpoint.location.country | ```HTTP_REQUEST_COUNTRY::VARCHAR``` |
| src_endpoint.name | ```HTTP_SOURCE_NAME::VARCHAR``` |
| src_endpoint.uid | ```HTTP_SOURCE_ID::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
