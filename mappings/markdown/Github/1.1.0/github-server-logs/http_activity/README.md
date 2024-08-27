# Event Dossier: Github Server Logs to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `github`
* Product name: `github-server-logs`
* Event codes: `PROTOCOL = 'http' OR REQUEST_METHOD IS NOT NULL`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE   WHEN REQUEST_METHOD = 'connect' THEN 1   WHEN REQUEST_METHOD = 'delete' THEN 2   WHEN REQUEST_METHOD = 'get' THEN 3   WHEN REQUEST_METHOD = 'head' THEN 4   WHEN REQUEST_METHOD = 'options' THEN 5   WHEN REQUEST_METHOD = 'post' THEN 6   WHEN REQUEST_METHOD = 'put' THEN 7   WHEN REQUEST_METHOD = 'trace' THEN 8 WHEN REQUEST_METHOD IS NULL THEN 0   ELSE 99  END::NUMBER``` |
| activity_name | ```CASE (CASE   WHEN REQUEST_METHOD = 'connect' THEN 1   WHEN REQUEST_METHOD = 'delete' THEN 2   WHEN REQUEST_METHOD = 'get' THEN 3   WHEN REQUEST_METHOD = 'head' THEN 4   WHEN REQUEST_METHOD = 'options' THEN 5   WHEN REQUEST_METHOD = 'post' THEN 6   WHEN REQUEST_METHOD = 'put' THEN 7   WHEN REQUEST_METHOD = 'trace' THEN 8 WHEN REQUEST_METHOD IS NULL THEN 0   ELSE 99  END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| app_name | ```APP::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(COALESCE(IP, REMOTE_ADDRESS), 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(COALESCE(IP, REMOTE_ADDRESS), 'INET'):family::NUMBER``` |
| connection_info.session.uid | ```RAW:user_session_id::VARCHAR``` |
| count | ```RAW:worker_request_count::NUMBER``` |
| dst_endpoint.type | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Server' WHEN 10 THEN 'Switch' WHEN 11 THEN 'Hub' WHEN 2 THEN 'Desktop' WHEN 3 THEN 'Laptop' WHEN 4 THEN 'Tablet' WHEN 5 THEN 'Mobile' WHEN 6 THEN 'Virtual' WHEN 7 THEN 'IOT' WHEN 8 THEN 'Browser' WHEN 9 THEN 'Firewall' WHEN 99 THEN 'Other' END``` |
| dst_endpoint.type_id | ```1::NUMBER``` |
| dst_endpoint.uid | ```RAW:server_id::VARCHAR``` |
| http_request.args | ```RAW:query_string::VARCHAR``` |
| http_request.http_method | ```CASE   WHEN REQUEST_METHOD = 'connect' THEN 'CONNECT'   WHEN REQUEST_METHOD = 'delete' THEN 'DELETE'   WHEN REQUEST_METHOD = 'get' THEN 'GET'   WHEN REQUEST_METHOD = 'head' THEN 'HEAD'   WHEN REQUEST_METHOD = 'options' THEN 'OPTIONS'   WHEN REQUEST_METHOD = 'post' THEN 'POST'   WHEN REQUEST_METHOD = 'put' THEN 'PUT'   WHEN REQUEST_METHOD = 'trace' THEN 'TRACE' ELSE NULL  END::VARCHAR``` |
| http_request.length | ```RAW:content_length::NUMBER``` |
| http_request.referrer | ```RAW:referer::VARCHAR``` |
| http_request.uid | ```REQUEST_ID::VARCHAR``` |
| http_request.url.hostname | ```REQUEST_HOST::VARCHAR``` |
| http_request.url.path | ```RAW:path_info::VARCHAR``` |
| http_request.url.query_string | ```RAW:query_string::VARCHAR``` |
| http_request.url.resource_type | ```REPO::VARCHAR``` |
| http_request.url.scheme | ```REGEXP_SUBSTR(URL, '^([a-zA-Z]+)')::VARCHAR``` |
| http_request.url.url_string | ```URL::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| http_request.x_forwarded_for | ```RAW:x_forwarded_for::VARCHAR``` |
| http_response.code | ```STATUS::NUMBER``` |
| http_status | ```STATUS::NUMBER``` |
| message | ```MESSAGE::VARCHAR``` |
| metadata.event_code | ```event_type``` |
| metadata.product.name | ```'github-server-logs'``` |
| metadata.product.vendor_name | ```'github'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```COALESCE(IP, REMOTE_ADDRESS)::VARCHAR``` |
| src_endpoint.name | ```RAW:user::VARCHAR``` |
| status | ```CASE (CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (CASE WHEN REQUEST_METHOD = 'connect' THEN 400201 WHEN REQUEST_METHOD = 'delete' THEN 400202 WHEN REQUEST_METHOD = 'get' THEN 400203 WHEN REQUEST_METHOD = 'head' THEN 400204 WHEN REQUEST_METHOD = 'options' THEN 400205 WHEN REQUEST_METHOD = 'post' THEN 400206 WHEN REQUEST_METHOD = 'put' THEN 400207 WHEN REQUEST_METHOD = 'trace' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN REQUEST_METHOD = 'connect' THEN 400201 WHEN REQUEST_METHOD = 'delete' THEN 400202 WHEN REQUEST_METHOD = 'get' THEN 400203 WHEN REQUEST_METHOD = 'head' THEN 400204 WHEN REQUEST_METHOD = 'options' THEN 400205 WHEN REQUEST_METHOD = 'post' THEN 400206 WHEN REQUEST_METHOD = 'put' THEN 400207 WHEN REQUEST_METHOD = 'trace' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
