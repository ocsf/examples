# Event Dossier: Squid Proxy Logs to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `squid`
* Product name: `squid-proxy-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE WHEN REQUEST_METHOD = 'NaN' THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN REQUEST_METHOD = 'NaN' THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```USER_EMAIL::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (CASE WHEN INTERNAL_IP is not null THEN 3 ELSE 2 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```CASE WHEN INTERNAL_IP is not null THEN 3 ELSE 2 END``` |
| dst_endpoint.ip | ```DESTINATION_IP::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT::VARCHAR``` |
| http_request.http_method | ```REQUEST_METHOD::VARCHAR``` |
| http_request.length | ```REQUEST_SIZE::NUMBER``` |
| http_request.url.scheme | ```URL_SCHEME::VARCHAR``` |
| http_request.url.url_string | ```REQUEST_URL::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT_DETAILS::VARCHAR``` |
| http_response.code | ```RESPONSE_STATUS_CODE::NUMBER``` |
| http_response.length | ```RESPONSE_SIZE::NUMBER``` |
| metadata.product.name | ```'squid-proxy-logs'``` |
| metadata.product.vendor_name | ```'squid'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', EVENT_TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```EVENT_TIME::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN RESPONSE_STATUS_CODE ILIKE '2%%' THEN 1 WHEN RESPONSE_STATUS_CODE IS NULL THEN 0 ELSE 2 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN RESPONSE_STATUS_CODE ILIKE '2%%' THEN 1 WHEN RESPONSE_STATUS_CODE IS NULL THEN 0 ELSE 2 END``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| traffic.bytes | ```RESPONSE_SIZE::NUMBER + REQUEST_SIZE::NUMBER``` |
| traffic.bytes_in | ```RESPONSE_SIZE::NUMBER``` |
| traffic.bytes_out | ```REQUEST_SIZE::NUMBER``` |
| type_name | ```CASE (CASE WHEN REQUEST_METHOD is null THEN 400200 WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 ELSE 4002099 END) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN REQUEST_METHOD is null THEN 400200 WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 ELSE 4002099 END``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
