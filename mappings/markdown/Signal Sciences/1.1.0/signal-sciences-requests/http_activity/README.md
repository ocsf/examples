# Event Dossier: Signal Sciences Requests to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `signal_sciences`
* Product name: `signal-sciences-requests`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN AGENT_RESPONSE_CODE = 200 THEN 1 WHEN AGENT_RESPONSE_CODE >= 301 THEN 2 WHEN AGENT_RESPONSE_CODE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN AGENT_RESPONSE_CODE = 200 THEN 1 WHEN AGENT_RESPONSE_CODE >= 301 THEN 2 WHEN AGENT_RESPONSE_CODE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN METHOD = 'CONNECT' THEN 1 WHEN METHOD = 'DELETE' THEN 2 WHEN METHOD = 'GET' THEN 3 WHEN METHOD = 'HEAD' THEN 4 WHEN METHOD = 'OPTIONS' THEN 5 WHEN METHOD = 'POST' THEN 6 WHEN METHOD = 'PUT' THEN 7 WHEN METHOD = 'TRACE' THEN 8 WHEN METHOD IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN METHOD = 'CONNECT' THEN 1 WHEN METHOD = 'DELETE' THEN 2 WHEN METHOD = 'GET' THEN 3 WHEN METHOD = 'HEAD' THEN 4 WHEN METHOD = 'OPTIONS' THEN 5 WHEN METHOD = 'POST' THEN 6 WHEN METHOD = 'PUT' THEN 7 WHEN METHOD = 'TRACE' THEN 8 WHEN METHOD IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```HEADERSOUT['X-AUSERNAME']::VARCHAR``` |
| actor.user.uid | ```HEADERSOUT['X-AUSERID']::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(REMOTE_IP, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(REMOTE_IP, 'INET'):family::NUMBER``` |
| disposition | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```0::NUMBER``` |
| dst_endpoint.name | ```SERVER_NAME::VARCHAR``` |
| firewall_rule.rate_limit | ```HEADERSOUT['X-RateLimit-Limit']::NUMBER``` |
| http_cookies.is_http_only | ```IFF(HEADERSOUT['Set-Cookie'] IS NOT NULL AND HEADERSOUT['Set-Cookie'] ILIKE '%%httponly;%%','true', 'false')::BOOLEAN``` |
| http_cookies.is_secure | ```IFF(HEADERSOUT['Set-Cookie'] IS NOT NULL AND HEADERSOUT['Set-Cookie'] ILIKE '%%secure;%%','true', 'false')::BOOLEAN``` |
| http_cookies.value | ```HEADERSOUT['Set-Cookie']::VARCHAR``` |
| http_request.http_method | ```CASE WHEN METHOD = 'CONNECT' THEN 'CONNECT' WHEN METHOD = 'DELETE' THEN 'DELETE' WHEN METHOD = 'GET' THEN 'GET' WHEN METHOD = 'HEAD' THEN 'HEAD' WHEN METHOD = 'OPTIONS' THEN 'OPTIONS' WHEN METHOD = 'POST' THEN 'POST' WHEN METHOD = 'PUT' THEN 'PUT' WHEN METHOD = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.length | ```TRY_TO_NUMERIC(TO_VARCHAR(HEADERSIN['Content-Length']))::NUMBER``` |
| http_request.referrer | ```HEADERSIN['referer']::VARCHAR``` |
| http_request.uid | ```ID::VARCHAR``` |
| http_request.url.hostname | ```HEADERSIN['Host']::VARCHAR``` |
| http_request.url.path | ```PATH::VARCHAR``` |
| http_request.url.port | ```HEADERSIN['X-Forwarded-Port']::VARCHAR``` |
| http_request.url.scheme | ```SCHEME::VARCHAR``` |
| http_request.url.url_string | ```URI::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| http_request.version | ```REGEXP_SUBSTR(PROTOCOL, '([0-9\.]+)')::VARCHAR``` |
| http_request.x_forwarded_for | ```HEADERSIN['X-Forwarded-For']::VARCHAR``` |
| http_response.code | ```RESPONSE_CODE::NUMBER``` |
| http_response.content_type | ```HEADERSOUT['content-type']::VARCHAR``` |
| http_response.latency | ```RESPONSE_MILLIS::NUMBER``` |
| http_response.length | ```RESPONSE_SIZE::NUMBER``` |
| load_balancer.code | ```AGENT_RESPONSE_CODE::NUMBER``` |
| load_balancer.status_detail | ```HEADERSIN['X-SigSci-Tags']::VARCHAR``` |
| metadata.event_code | ```method``` |
| metadata.product.name | ```'signal-sciences-requests'``` |
| metadata.product.vendor_name | ```'signal_sciences'``` |
| metadata.version | ```'1.1.0'``` |
| proxy_endpoint.hostname | ```SERVER_HOSTNAME::VARCHAR``` |
| proxy_http_request.uid | ```HEADERSIN['X-Request-ID']::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.hostname | ```REMOTE_HOSTNAME::VARCHAR``` |
| src_endpoint.ip | ```REMOTE_IP::VARCHAR``` |
| src_endpoint.location.country | ```REMOTE_COUNTRY_CODE::VARCHAR``` |
| status | ```CASE (CASE WHEN RESPONSE_CODE ILIKE '2%%' THEN 1 WHEN RESPONSE_CODE ILIKE '4%%' THEN 2 WHEN RESPONSE_CODE ILIKE '5%%' THEN 2 WHEN RESPONSE_CODE IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN RESPONSE_CODE ILIKE '2%%' THEN 1 WHEN RESPONSE_CODE ILIKE '4%%' THEN 2 WHEN RESPONSE_CODE ILIKE '5%%' THEN 2 WHEN RESPONSE_CODE IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', timestamp::TIMESTAMP_LTZ)``` |
| time_dt | ```timestamp::TIMESTAMP_LTZ``` |
| tls.cipher | ```TLS_CIPHER::VARCHAR``` |
| tls.version | ```TLS_PROTOCOL::VARCHAR``` |
| traffic.bytes | ```TRY_TO_NUMERIC(TO_VARCHAR(HEADERSIN['Content-Length'])) + RESPONSE_SIZE::NUMBER``` |
| traffic.bytes_in | ```TRY_TO_NUMERIC(TO_VARCHAR(HEADERSIN['Content-Length']))::NUMBER``` |
| traffic.bytes_out | ```RESPONSE_SIZE::NUMBER``` |
| type_name | ```CASE (CASE WHEN METHOD = 'CONNECT' THEN 400201 WHEN METHOD = 'DELETE' THEN 400202 WHEN METHOD = 'GET' THEN 400203 WHEN METHOD = 'HEAD' THEN 400204 WHEN METHOD = 'OPTIONS' THEN 400205 WHEN METHOD = 'POST' THEN 400206 WHEN METHOD = 'PUT' THEN 400207 WHEN METHOD = 'TRACE' THEN 400208 WHEN METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN METHOD = 'CONNECT' THEN 400201 WHEN METHOD = 'DELETE' THEN 400202 WHEN METHOD = 'GET' THEN 400203 WHEN METHOD = 'HEAD' THEN 400204 WHEN METHOD = 'OPTIONS' THEN 400205 WHEN METHOD = 'POST' THEN 400206 WHEN METHOD = 'PUT' THEN 400207 WHEN METHOD = 'TRACE' THEN 400208 WHEN METHOD IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
