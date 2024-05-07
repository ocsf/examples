# Event Dossier: Signal Sciences Events to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `signal_sciences`
* Product name: `signal-sciences-events`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION = 'info' THEN 1 WHEN ACTION = 'flagged' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION = 'info' THEN 1 WHEN ACTION = 'flagged' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN REQUEST_METHOD = 'UNKNOWN' THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD  = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN REQUEST_METHOD = 'UNKNOWN' THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD  = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(SOURCE_IP, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(SOURCE_IP, 'INET'):family::NUMBER``` |
| dst_endpoint.hostname | ```REQUEST_SERVER_HOSTNAME::VARCHAR``` |
| dst_endpoint.location.country | ```REMOTE_COUNTRY_CODE::VARCHAR``` |
| dst_endpoint.name | ```REQUEST_SERVER_NAME::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', EXPIRES::TIMESTAMP_LTZ)``` |
| end_time_dt | ```EXPIRES::TIMESTAMP_LTZ``` |
| http_cookies.name | ```REQUEST_HEADERSIN:cookie::VARCHAR``` |
| http_request.http_method | ```CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 'CONNECT' WHEN REQUEST_METHOD = 'DELETE' THEN 'DELETE' WHEN REQUEST_METHOD = 'GET' THEN 'GET' WHEN REQUEST_METHOD = 'HEAD' THEN 'HEAD' WHEN REQUEST_METHOD = 'OPTIONS' THEN 'OPTIONS' WHEN REQUEST_METHOD = 'POST' THEN 'POST' WHEN REQUEST_METHOD = 'PUT' THEN 'PUT' WHEN REQUEST_METHOD = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.referrer | ```REQUEST_HEADERSIN:referer::VARCHAR``` |
| http_request.url.path | ```REQUEST_PATH::VARCHAR``` |
| http_request.url.scheme | ```REQUEST_SCHEME::VARCHAR``` |
| http_request.user_agent | ```USER_AGENTS::VARCHAR``` |
| http_request.version | ```REQUEST_PROTOCOL::VARCHAR``` |
| http_request.x_forwarded_for | ```REQUEST_HEADERSIN:"X-Forwarded-For"::VARCHAR``` |
| http_response.code | ```REQUEST_RESPONSE_CODE::NUMBER``` |
| http_response.content_type | ```REQUEST_HEADERSOUT:"content-type"::VARCHAR``` |
| http_response.latency | ```REQUEST_RESPONSE_MILLIS::NUMBER``` |
| http_response.length | ```REQUEST_RESPONSE_SIZE::NUMBER``` |
| metadata.event_code | ```EVENT_TYPE``` |
| metadata.product.name | ```'signal-sciences-events'``` |
| metadata.product.vendor_name | ```'signal_sciences'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.hostname | ```REMOTE_HOSTNAME::VARCHAR``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| status | ```CASE (CASE WHEN REQUEST_RESPONSE_CODE ILIKE '2%%' THEN 1 WHEN REQUEST_RESPONSE_CODE ILIKE '4%%' THEN 2 WHEN REQUEST_RESPONSE_CODE ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN REQUEST_RESPONSE_CODE ILIKE '2%%' THEN 1 WHEN REQUEST_RESPONSE_CODE ILIKE '4%%' THEN 2 WHEN REQUEST_RESPONSE_CODE ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| tls.server_ciphers | ```REQUEST_TLS_CIPHER::VARCHAR``` |
| tls.version | ```REQUEST_TLS_PROTOCOL::VARCHAR``` |
| type_name | ```CASE (CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
