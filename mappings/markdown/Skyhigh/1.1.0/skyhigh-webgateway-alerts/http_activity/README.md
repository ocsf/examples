# Event Dossier: Skyhigh Webgateway Alerts to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `skyhigh`
* Product name: `skyhigh-webgateway-alerts`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN BLOCK_RESULT = 0 THEN 1 WHEN BLOCK_RESULT = 10 THEN 2 WHEN BLOCK_RESULT = 22 THEN 2 WHEN BLOCK_RESULT = 81 THEN 2 WHEN BLOCK_RESULT = 103 THEN 2 WHEN BLOCK_RESULT IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN BLOCK_RESULT = 0 THEN 1 WHEN BLOCK_RESULT = 10 THEN 2 WHEN BLOCK_RESULT = 22 THEN 2 WHEN BLOCK_RESULT = 81 THEN 2 WHEN BLOCK_RESULT = 103 THEN 2 WHEN BLOCK_RESULT IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN METHOD = 'UNKNOWN' THEN 0 WHEN METHOD = 'CONNECT' THEN 1 WHEN METHOD = 'DELETE' THEN 2 WHEN METHOD = 'GET' THEN 3 WHEN METHOD = 'HEAD' THEN 4 WHEN METHOD = 'OPTIONS' THEN 5 WHEN METHOD = 'POST' THEN 6 WHEN METHOD = 'PUT' THEN 7 WHEN METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN METHOD = 'UNKNOWN' THEN 0 WHEN METHOD = 'CONNECT' THEN 1 WHEN METHOD = 'DELETE' THEN 2 WHEN METHOD = 'GET' THEN 3 WHEN METHOD = 'HEAD' THEN 4 WHEN METHOD = 'OPTIONS' THEN 5 WHEN METHOD = 'POST' THEN 6 WHEN METHOD = 'PUT' THEN 7 WHEN METHOD = 'TRACE' THEN 8 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```AUTH_USER::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.boundary | ```CASE (5::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Localhost' WHEN 10 THEN 'Gateway VPC' WHEN 11 THEN 'Internet Gateway' WHEN 2 THEN 'Internal' WHEN 3 THEN 'External' WHEN 4 THEN 'Same VPC' WHEN 5 THEN 'Internet/VPC Gateway' WHEN 6 THEN 'Virtual Private Gateway' WHEN 7 THEN 'Intra-region VPC' WHEN 8 THEN 'Inter-region VPC' WHEN 9 THEN 'Local Gateway' WHEN 99 THEN 'Other' END``` |
| connection_info.boundary_id | ```5::NUMBER``` |
| connection_info.direction | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```2::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(SOURCE_IP, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(SOURCE_IP, 'INET'):family::NUMBER``` |
| dst_endpoint.ip | ```SERVER_IP::VARCHAR``` |
| http_request.http_method | ```CASE WHEN METHOD = 'CONNECT' THEN 'CONNECT' WHEN METHOD = 'DELETE' THEN 'DELETE' WHEN METHOD = 'GET' THEN 'GET' WHEN METHOD = 'HEAD' THEN 'HEAD' WHEN METHOD = 'OPTIONS' THEN 'OPTIONS' WHEN METHOD = 'POST' THEN 'POST' WHEN METHOD = 'PUT' THEN 'PUT' WHEN METHOD = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.length | ```BYTES_FROM_CLIENT::NUMBER``` |
| http_request.url.hostname | ```HOST::VARCHAR``` |
| http_request.url.port | ```URL_PORT::VARCHAR``` |
| http_request.url.url_string | ```URL::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| http_response.code | ```STATUS_CODE::NUMBER``` |
| http_response.length | ```BYTES_TO_CLIENT::NUMBER``` |
| metadata.product.name | ```'skyhigh-webgateway-alerts'``` |
| metadata.product.vendor_name | ```'skyhigh'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| status | ```CASE (CASE WHEN STATUS_CODE ILIKE '2%%' THEN 1 WHEN STATUS_CODE ILIKE '3%%' THEN 2 WHEN STATUS_CODE ILIKE '4%%' THEN 2 WHEN STATUS_CODE ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN STATUS_CODE ILIKE '2%%' THEN 1 WHEN STATUS_CODE ILIKE '3%%' THEN 2 WHEN STATUS_CODE ILIKE '4%%' THEN 2 WHEN STATUS_CODE ILIKE '5%%' THEN 2 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', time_stamp::TIMESTAMP_LTZ)``` |
| time_dt | ```time_stamp::TIMESTAMP_LTZ``` |
| traffic.bytes | ```(COALESCE(BYTES_FROM_CLIENT, 0) + COALESCE(BYTES_TO_CLIENT, 0))::NUMBER``` |
| traffic.bytes_in | ```BYTES_TO_CLIENT::NUMBER``` |
| traffic.bytes_out | ```BYTES_FROM_CLIENT::NUMBER``` |
| type_name | ```CASE (CASE WHEN METHOD = 'CONNECT' THEN 400201 WHEN METHOD = 'DELETE' THEN 400202 WHEN METHOD = 'GET' THEN 400203 WHEN METHOD = 'HEAD' THEN 400204 WHEN METHOD = 'OPTIONS' THEN 400205 WHEN METHOD = 'POST' THEN 400206 WHEN METHOD = 'PUT' THEN 400207 WHEN METHOD = 'TRACE' THEN 400208 WHEN METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN METHOD = 'CONNECT' THEN 400201 WHEN METHOD = 'DELETE' THEN 400202 WHEN METHOD = 'GET' THEN 400203 WHEN METHOD = 'HEAD' THEN 400204 WHEN METHOD = 'OPTIONS' THEN 400205 WHEN METHOD = 'POST' THEN 400206 WHEN METHOD = 'PUT' THEN 400207 WHEN METHOD = 'TRACE' THEN 400208 WHEN METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
