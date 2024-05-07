# Event Dossier: Alibaba Slb Logs to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `alibaba`
* Product name: `alibaba-slb-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE WHEN REQUEST_METHOD = 'UNKNOWN' THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN REQUEST_METHOD = 'UNKNOWN' THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(CLIENT_IP, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(CLIENT_IP, 'INET'):family::NUMBER``` |
| dst_endpoint.ip | ```VIP_ADDR::VARCHAR``` |
| dst_endpoint.port | ```SLB_VPORT::VARCHAR``` |
| duration | ```TCPINFO_RTT::NUMBER``` |
| http_request.http_method | ```CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 'CONNECT' WHEN REQUEST_METHOD = 'DELETE' THEN 'DELETE' WHEN REQUEST_METHOD = 'GET' THEN 'GET' WHEN REQUEST_METHOD = 'HEAD' THEN 'HEAD' WHEN REQUEST_METHOD = 'OPTIONS' THEN 'OPTIONS' WHEN REQUEST_METHOD = 'POST' THEN 'POST' WHEN REQUEST_METHOD = 'PUT' THEN 'PUT' WHEN REQUEST_METHOD = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.length | ```REQUEST_LENGTH::NUMBER``` |
| http_request.referrer | ```HTTP_REFERER::VARCHAR``` |
| http_request.url.hostname | ```HTTP_HOST::VARCHAR``` |
| http_request.url.path | ```REQUEST_URI::VARCHAR``` |
| http_request.url.scheme | ```SCHEME::VARCHAR``` |
| http_request.user_agent | ```HTTP_USER_AGENT::VARCHAR``` |
| http_request.version | ```SERVER_PROTOCOL::VARCHAR``` |
| http_request.x_forwarded_for | ```HTTP_X_FORWARDED_FOR::VARCHAR``` |
| http_response.code | ```STATUS::NUMBER``` |
| load_balancer.code | ```UPSTREAM_STATUS::NUMBER``` |
| load_balancer.uid | ```SLBID::VARCHAR``` |
| metadata.product.name | ```'alibaba-slb-logs'``` |
| metadata.product.vendor_name | ```'alibaba'``` |
| metadata.version | ```'1.1.0'``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| src_endpoint.port | ```CLIENT_PORT::VARCHAR``` |
| status | ```CASE (CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '3%%' THEN 2 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS ILIKE '2%%' THEN 1 WHEN STATUS ILIKE '3%%' THEN 2 WHEN STATUS ILIKE '4%%' THEN 2 WHEN STATUS ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', time::TIMESTAMP_LTZ)``` |
| time_dt | ```time::TIMESTAMP_LTZ``` |
| tls.cipher | ```SSL_CIPHER::VARCHAR``` |
| tls.version | ```SSL_PROTOCOL::VARCHAR``` |
| traffic.bytes | ```(COALESCE(REQUEST_LENGTH, 0) + COALESCE(BODY_BYTES_SENT, 0))::NUMBER``` |
| traffic.bytes_in | ```REQUEST_LENGTH::NUMBER``` |
| traffic.bytes_out | ```BODY_BYTES_SENT::NUMBER``` |
| type_name | ```CASE (CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN REQUEST_METHOD = 'CONNECT' THEN 400201 WHEN REQUEST_METHOD = 'DELETE' THEN 400202 WHEN REQUEST_METHOD = 'GET' THEN 400203 WHEN REQUEST_METHOD = 'HEAD' THEN 400204 WHEN REQUEST_METHOD = 'OPTIONS' THEN 400205 WHEN REQUEST_METHOD = 'POST' THEN 400206 WHEN REQUEST_METHOD = 'PUT' THEN 400207 WHEN REQUEST_METHOD = 'TRACE' THEN 400208 WHEN REQUEST_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
