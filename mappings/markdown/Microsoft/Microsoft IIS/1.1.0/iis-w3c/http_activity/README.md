# Event Dossier: Iis W3c to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `Microsoft IIS`
* Product name: `iis-w3c`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```DECODE(METHOD, 'CONNECT', 1, 'DELETE', 2, 'GET', 3,'HEAD', 4, 'OPTIONS', 5, 'POST', 6, 'PUT', 7, 'TRACE', 8,0)``` |
| activity_name | ```CASE (DECODE(METHOD, 'CONNECT', 1, 'DELETE', 2, 'GET', 3,'HEAD', 4, 'OPTIONS', 5, 'POST', 6, 'PUT', 7, 'TRACE', 8,0)) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```USERNAME::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| dst_endpoint.ip | ```SERVER_IP::VARCHAR``` |
| dst_endpoint.name | ```SERVER_NAME::VARCHAR``` |
| dst_endpoint.port | ```SERVER_PORT::VARCHAR``` |
| duration | ```TIME_TAKEN::NUMBER``` |
| http_cookies.name | ```COOKIE::VARCHAR``` |
| http_request.http_method | ```METHOD::VARCHAR``` |
| http_request.length | ```BYTES_SENT::NUMBER``` |
| http_request.referrer | ```REFERRER::VARCHAR``` |
| http_request.url.query_string | ```URI_QUERY::VARCHAR``` |
| http_request.url.url_string | ```URI_STEM::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| http_response.code | ```STATUS_CODE::NUMBER``` |
| http_response.length | ```BYTES_RECEIVED::NUMBER``` |
| metadata.product.name | ```'iis-w3c'``` |
| metadata.product.vendor_name | ```'Microsoft IIS'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| status | ```CASE (CASE WHEN STATUS_CODE ILIKE '2%%' THEN 1 WHEN STATUS_CODE ILIKE  '4%%' THEN 2 WHEN STATUS_CODE ILIKE '5%%' THEN 2 WHEN STATUS_CODE IS NULL THEN 0 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_code | ```STATUS_CODE::VARCHAR``` |
| status_id | ```CASE WHEN STATUS_CODE ILIKE '2%%' THEN 1 WHEN STATUS_CODE ILIKE  '4%%' THEN 2 WHEN STATUS_CODE ILIKE '5%%' THEN 2 WHEN STATUS_CODE IS NULL THEN 0 ELSE 99 END``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE (DECODE(METHOD, 'CONNECT', 400201, 'DELETE', 400202, 'GET', 400203,'HEAD', 400204, 'OPTIONS', 400205, 'POST', 400206, 'PUT', 400207, 'TRACE', 400208,400200)) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```DECODE(METHOD, 'CONNECT', 400201, 'DELETE', 400202, 'GET', 400203,'HEAD', 400204, 'OPTIONS', 400205, 'POST', 400206, 'PUT', 400207, 'TRACE', 400208,400200)``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
