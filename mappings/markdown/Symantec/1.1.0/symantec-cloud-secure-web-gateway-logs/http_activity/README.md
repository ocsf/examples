# Event Dossier: Symantec Cloud Secure Web Gateway Logs to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `symantec`
* Product name: `symantec-cloud-secure-web-gateway-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN SERVER_ACTION = 'TUNNELED' THEN 1 WHEN SERVER_ACTION = 'TCP_TUNNELED' THEN 1 WHEN SERVER_ACTION = 'DENIED' THEN 2 WHEN SERVER_ACTION = 'FAILED' THEN 2 WHEN SERVER_ACTION = 'TCP_DENIED' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN SERVER_ACTION = 'TUNNELED' THEN 1 WHEN SERVER_ACTION = 'TCP_TUNNELED' THEN 1 WHEN SERVER_ACTION = 'DENIED' THEN 2 WHEN SERVER_ACTION = 'FAILED' THEN 2 WHEN SERVER_ACTION = 'TCP_DENIED' THEN 2 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN CLIENT_TO_SERVER_METHOD = 'UNKNOWN' THEN 0 WHEN CLIENT_TO_SERVER_METHOD = 'CONNECT' THEN 1 WHEN CLIENT_TO_SERVER_METHOD = 'DELETE' THEN 2 WHEN CLIENT_TO_SERVER_METHOD = 'GET' THEN 3 WHEN CLIENT_TO_SERVER_METHOD = 'HEAD' THEN 4 WHEN CLIENT_TO_SERVER_METHOD = 'OPTIONS' THEN 5 WHEN CLIENT_TO_SERVER_METHOD = 'POST' THEN 6 WHEN CLIENT_TO_SERVER_METHOD = 'PUT' THEN 7 WHEN CLIENT_TO_SERVER_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN CLIENT_TO_SERVER_METHOD = 'UNKNOWN' THEN 0 WHEN CLIENT_TO_SERVER_METHOD = 'CONNECT' THEN 1 WHEN CLIENT_TO_SERVER_METHOD = 'DELETE' THEN 2 WHEN CLIENT_TO_SERVER_METHOD = 'GET' THEN 3 WHEN CLIENT_TO_SERVER_METHOD = 'HEAD' THEN 4 WHEN CLIENT_TO_SERVER_METHOD = 'OPTIONS' THEN 5 WHEN CLIENT_TO_SERVER_METHOD = 'POST' THEN 6 WHEN CLIENT_TO_SERVER_METHOD = 'PUT' THEN 7 WHEN CLIENT_TO_SERVER_METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```CLIENT_TO_SERVER_USERDN::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.boundary | ```CASE (5::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Localhost' WHEN 10 THEN 'Gateway VPC' WHEN 11 THEN 'Internet Gateway' WHEN 2 THEN 'Internal' WHEN 3 THEN 'External' WHEN 4 THEN 'Same VPC' WHEN 5 THEN 'Internet/VPC Gateway' WHEN 6 THEN 'Virtual Private Gateway' WHEN 7 THEN 'Intra-region VPC' WHEN 8 THEN 'Inter-region VPC' WHEN 9 THEN 'Local Gateway' WHEN 99 THEN 'Other' END``` |
| connection_info.boundary_id | ```5::NUMBER``` |
| connection_info.direction | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```2::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(CLIENT_IP, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(CLIENT_IP, 'INET'):family::NUMBER``` |
| device.name | ```CLIENT_DEVICE_NAME::VARCHAR``` |
| dst_endpoint.ip | ```RESPONSE_IP::VARCHAR``` |
| dst_endpoint.location.country | ```RESPONSE_SUPPLIER_COUNTRY::VARCHAR``` |
| http_request.http_method | ```CASE WHEN CLIENT_TO_SERVER_METHOD = 'CONNECT' THEN 'CONNECT' WHEN CLIENT_TO_SERVER_METHOD = 'DELETE' THEN 'DELETE' WHEN CLIENT_TO_SERVER_METHOD = 'GET' THEN 'GET' WHEN CLIENT_TO_SERVER_METHOD = 'HEAD' THEN 'HEAD' WHEN CLIENT_TO_SERVER_METHOD = 'OPTIONS' THEN 'OPTIONS' WHEN CLIENT_TO_SERVER_METHOD = 'POST' THEN 'POST' WHEN CLIENT_TO_SERVER_METHOD = 'PUT' THEN 'PUT' WHEN CLIENT_TO_SERVER_METHOD = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.length | ```CLIENT_TO_SERVER_BYTES::NUMBER``` |
| http_request.referrer | ```CLIENT_TO_SERVER_REQUEST_HEADER_REFERER::VARCHAR``` |
| http_request.url.hostname | ```CLIENT_TO_SERVER_HOST::VARCHAR``` |
| http_request.url.path | ```CLIENT_TO_SERVER_URI_PATH::VARCHAR``` |
| http_request.url.port | ```CLIENT_TO_SERVER_URI_PORT::VARCHAR``` |
| http_request.url.query_string | ```CLIENT_TO_SERVER_URI_QUERY::VARCHAR``` |
| http_request.url.scheme | ```CLIENT_TO_SERVER_URI_SCHEME::VARCHAR``` |
| http_request.user_agent | ```CLIENT_TO_SERVER_USER_AGENT::VARCHAR``` |
| http_response.code | ```SERVER_TO_CLIENT_STATUS::NUMBER``` |
| http_response.content_type | ```RESPONSE_HEADER_CONTENT_TYPE::VARCHAR``` |
| http_response.length | ```SERVER_TO_CLIENT_BYTES::NUMBER``` |
| metadata.product.name | ```'symantec-cloud-secure-web-gateway-logs'``` |
| metadata.product.vendor_name | ```'symantec'``` |
| metadata.version | ```'1.1.0'``` |
| proxy_endpoint.ip | ```SERVER_IP::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| status | ```CASE (CASE WHEN SERVER_TO_CLIENT_STATUS ILIKE '2%%' THEN 1 WHEN SERVER_TO_CLIENT_STATUS ILIKE '4%%' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN SERVER_TO_CLIENT_STATUS ILIKE '2%%' THEN 1 WHEN SERVER_TO_CLIENT_STATUS ILIKE '4%%' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| tls.client_ciphers | ```CLIENT_TO_SERVER_CONNECTION_NEGOTIATED_CIPHER::VARCHAR``` |
| tls.server_ciphers | ```RESPONSE_CONNECTION_NEGOTIATED_CIPHER::VARCHAR``` |
| traffic.bytes_in | ```SERVER_TO_CLIENT_BYTES::NUMBER``` |
| traffic.bytes_out | ```CLIENT_TO_SERVER_BYTES::NUMBER``` |
| type_name | ```CASE (CASE WHEN CLIENT_TO_SERVER_METHOD = 'CONNECT' THEN 400201 WHEN CLIENT_TO_SERVER_METHOD = 'DELETE' THEN 400202 WHEN CLIENT_TO_SERVER_METHOD = 'GET' THEN 400203 WHEN CLIENT_TO_SERVER_METHOD = 'HEAD' THEN 400204 WHEN CLIENT_TO_SERVER_METHOD = 'OPTIONS' THEN 400205 WHEN CLIENT_TO_SERVER_METHOD = 'POST' THEN 400206 WHEN CLIENT_TO_SERVER_METHOD = 'PUT' THEN 400207 WHEN CLIENT_TO_SERVER_METHOD = 'TRACE' THEN 400208 WHEN CLIENT_TO_SERVER_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN CLIENT_TO_SERVER_METHOD = 'CONNECT' THEN 400201 WHEN CLIENT_TO_SERVER_METHOD = 'DELETE' THEN 400202 WHEN CLIENT_TO_SERVER_METHOD = 'GET' THEN 400203 WHEN CLIENT_TO_SERVER_METHOD = 'HEAD' THEN 400204 WHEN CLIENT_TO_SERVER_METHOD = 'OPTIONS' THEN 400205 WHEN CLIENT_TO_SERVER_METHOD = 'POST' THEN 400206 WHEN CLIENT_TO_SERVER_METHOD = 'PUT' THEN 400207 WHEN CLIENT_TO_SERVER_METHOD = 'TRACE' THEN 400208 WHEN CLIENT_TO_SERVER_METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
