# Event Dossier: Imperva Waf Logs to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `imperva`
* Product name: `imperva-waf-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE WHEN METHOD is NULL THEN 0 WHEN METHOD = 'Connect' THEN 1 WHEN METHOD = 'Delete' THEN 2 WHEN METHOD = 'Get' THEN 3 WHEN METHOD = 'Head' THEN 4 WHEN METHOD = 'Options' THEN 5 WHEN METHOD = 'Post' THEN 6 WHEN METHOD = 'Put' THEN 7 WHEN METHOD = 'Trace' THEN 8 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN METHOD is NULL THEN 0 WHEN METHOD = 'Connect' THEN 1 WHEN METHOD = 'Delete' THEN 2 WHEN METHOD = 'Get' THEN 3 WHEN METHOD = 'Head' THEN 4 WHEN METHOD = 'Options' THEN 5 WHEN METHOD = 'Post' THEN 6 WHEN METHOD = 'Put' THEN 7 WHEN METHOD = 'Trace' THEN 8 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| app_name | ```CLAPP::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| device.zone | ```POP_NAME::VARCHAR``` |
| dst_endpoint.domain | ```SITE_NAME::VARCHAR``` |
| dst_endpoint.ip | ```SIP::VARCHAR``` |
| dst_endpoint.location.coordinates | ```ARRAY_CONSTRUCT(LONGITUDE, LATITUDE)``` |
| dst_endpoint.location.country | ```COUNTRY_CODE::VARCHAR``` |
| dst_endpoint.port | ```SPT::VARCHAR``` |
| dst_endpoint.zone | ```POP_NAME::VARCHAR``` |
| end_time | ```date_part('epoch_milliseconds', RESPONSE_END_TIME::TIMESTAMP_LTZ)``` |
| end_time_dt | ```RESPONSE_END_TIME::TIMESTAMP_LTZ``` |
| http_request.http_method | ```METHOD::VARCHAR``` |
| http_request.length | ```CONTENT_LENGTH::NUMBER``` |
| http_request.referrer | ```REFERRER::VARCHAR``` |
| http_request.uid | ```REQUEST_ID::VARCHAR``` |
| http_request.url.hostname | ```SPLIT_PART(URL, '/', 1)::VARCHAR``` |
| http_request.url.path | ```REGEXP_SUBSTR(URL, '/[^? ]+')::VARCHAR``` |
| http_request.url.url_string | ```URL::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| http_request.x_forwarded_for | ```X_FORWARDED_FOR::VARCHAR``` |
| http_response.code | ```HTTP_STATUS_CODE::NUMBER``` |
| http_response.message | ```REQUEST_RESULT::VARCHAR``` |
| http_status | ```HTTP_STATUS_CODE::NUMBER``` |
| metadata.product.name | ```'imperva-waf-logs'``` |
| metadata.product.vendor_name | ```'imperva'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (CASE WHEN 'SEVERITY' IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN 'SEVERITY' IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| src_endpoint.port | ```SOURCE_PORT::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', REQUEST_START_TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```REQUEST_START_TIME::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN HTTP_STATUS_CODE ILIKE '2%%' THEN 1 WHEN HTTP_STATUS_CODE ILIKE '4%%' THEN 2 WHEN HTTP_STATUS_CODE ILIKE '5%%' THEN 2 WHEN HTTP_STATUS_CODE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN HTTP_STATUS_CODE ILIKE '2%%' THEN 1 WHEN HTTP_STATUS_CODE ILIKE '4%%' THEN 2 WHEN HTTP_STATUS_CODE ILIKE '5%%' THEN 2 WHEN HTTP_STATUS_CODE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', request_start_time::TIMESTAMP_LTZ)``` |
| time_dt | ```request_start_time::TIMESTAMP_LTZ``` |
| tls.version | ```PROTOCOL_VERSION::VARCHAR``` |
| type_name | ```CASE (CASE WHEN METHOD = 'CONNECT' THEN 400201 WHEN METHOD = 'DELETE' THEN 400202 WHEN METHOD = 'GET' THEN 400203 WHEN METHOD = 'HEAD' THEN 400204 WHEN METHOD = 'OPTIONS' THEN 400205 WHEN METHOD = 'POST' THEN 400206 WHEN METHOD = 'PUT' THEN 400207 WHEN METHOD = 'TRACE' THEN 400208 WHEN METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN METHOD = 'CONNECT' THEN 400201 WHEN METHOD = 'DELETE' THEN 400202 WHEN METHOD = 'GET' THEN 400203 WHEN METHOD = 'HEAD' THEN 400204 WHEN METHOD = 'OPTIONS' THEN 400205 WHEN METHOD = 'POST' THEN 400206 WHEN METHOD = 'PUT' THEN 400207 WHEN METHOD = 'TRACE' THEN 400208 WHEN METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
