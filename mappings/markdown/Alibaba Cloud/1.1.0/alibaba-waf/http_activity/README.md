# Event Dossier: Alibaba Waf to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `alibaba`
* Product name: `alibaba-waf`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN RAW:final_action::VARCHAR IS NULL THEN 1 WHEN RAW:final_action::VARCHAR = 'Block' THEN 2 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN RAW:final_action::VARCHAR IS NULL THEN 1 WHEN RAW:final_action::VARCHAR = 'Block' THEN 2 ELSE 99 END``` |
| activity_id | ```CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 WHEN REQUEST_METHOD IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 WHEN REQUEST_METHOD IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.user.uid | ```USER_ID::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| cloud.provider | ```'Alibaba'::VARCHAR``` |
| cloud.region | ```REGION::VARCHAR``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| disposition | ```CASE (CASE WHEN RAW:final_action IS NULL THEN 1 WHEN RAW:final_action = 'Block' THEN 2 ELSE 99 END :: NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```CASE WHEN RAW:final_action IS NULL THEN 1 WHEN RAW:final_action = 'Block' THEN 2 ELSE 99 END :: NUMBER``` |
| dst_endpoint.hostname | ```HOST::VARCHAR``` |
| dst_endpoint.ip | ```REMOTE_ADDR::VARCHAR``` |
| dst_endpoint.port | ```REMOTE_PORT::VARCHAR``` |
| duration | ```REQUEST_TIME_MSEC::NUMBER``` |
| http_cookies.value | ```HTTP_COOKIE::VARCHAR``` |
| http_request.http_method | ```REQUEST_METHOD::VARCHAR``` |
| http_request.length | ```REQUEST_LENGTH::NUMBER``` |
| http_request.referrer | ```HTTP_REFERER::VARCHAR``` |
| http_request.url.hostname | ```HOST::VARCHAR``` |
| http_request.url.path | ```REQUEST_PATH::VARCHAR``` |
| http_request.url.query_string | ```QUERYSTRING::VARCHAR``` |
| http_request.url.scheme | ```SERVER_PROTOCOL::VARCHAR``` |
| http_request.user_agent | ```HTTP_USER_AGENT::VARCHAR``` |
| http_request.version | ```SERVER_PROTOCOL::VARCHAR``` |
| http_request.x_forwarded_for | ```HTTP_X_FORWARDED_FOR::VARCHAR``` |
| http_response.status | ```STATUS::VARCHAR``` |
| metadata.product.name | ```'alibaba-waf'``` |
| metadata.product.vendor_name | ```'alibaba'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```REAL_CLIENT_IP::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```TIME::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS ILIKE '5%%' THEN 2 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS ILIKE '5%%' THEN 2 ELSE 99 END``` |
| time | ```date_part('epoch_milliseconds', time::TIMESTAMP_LTZ)``` |
| time_dt | ```time::TIMESTAMP_LTZ``` |
| tls.cipher | ```SSL_CIPHER::VARCHAR``` |
| tls.version | ```SSL_PROTOCOL::VARCHAR``` |
| traffic.bytes_out | ```BODY_BYTES_SENT::NUMBER``` |
| type_name | ```CASE (CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
