# Event Dossier: Oracle Service Logs to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `oracle`
* Product name: `oracle-service-logs`
* Event codes: `event_type = 'com.oraclecloud.loadbalancer.waf'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'block' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'block' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN RAW:data:request:method = 'CONNECT' THEN 1 WHEN RAW:data:request:method = 'DELETE' THEN 2 WHEN RAW:data:request:method = 'GET' THEN 3 WHEN RAW:data:request:method = 'HEAD' THEN 4 WHEN RAW:data:request:method = 'OPTIONS' THEN 5 WHEN RAW:data:request:method = 'POST' THEN 6 WHEN RAW:data:request:method = 'PUT' THEN 7 WHEN RAW:data:request:method = 'TRACE' THEN 8 WHEN RAW:data:request:method IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN RAW:data:request:method = 'CONNECT' THEN 1 WHEN RAW:data:request:method = 'DELETE' THEN 2 WHEN RAW:data:request:method = 'GET' THEN 3 WHEN RAW:data:request:method = 'HEAD' THEN 4 WHEN RAW:data:request:method = 'OPTIONS' THEN 5 WHEN RAW:data:request:method = 'POST' THEN 6 WHEN RAW:data:request:method = 'PUT' THEN 7 WHEN RAW:data:request:method = 'TRACE' THEN 8 WHEN RAW:data:request:method IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| cloud.account.uid | ```TENANT_ID::VARCHAR``` |
| cloud.org.name | ```'Oracle'::VARCHAR``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(RAW:data:clientAddr, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(RAW:data:clientAddr, 'INET'):family::NUMBER``` |
| connection_info.uid | ```ID::VARCHAR``` |
| disposition | ```CASE (CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'block' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```CASE WHEN ACTION = 'allow' THEN 1 WHEN ACTION = 'block' THEN 2 WHEN ACTION IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| dst_endpoint.hostname | ```RAW:data:responseProvider::VARCHAR``` |
| dst_endpoint.ip | ```IFF(RAW:data:responseProvider ILIKE '%%:%%', SPLIT_PART(RAW:data:responseProvider, ':', 1), NULL)::VARCHAR``` |
| dst_endpoint.port | ```IFF(RAW:data:responseProvider ILIKE '%%:%%', SPLIT_PART(RAW:data:responseProvider, ':', 2), NULL)::VARCHAR``` |
| firewall_rule.match_details | ```RAW:data:requestProtection:matchedRules::VARCHAR``` |
| firewall_rule.uid | ```RAW:data:requestProtection:matchedIds::VARCHAR``` |
| http_cookies.http_only | ```IFF(RAW:data:request:cookie IS NOT NULL AND RAW:data:request:cookie ILIKE '%%httponly;%%','true', 'false')::BOOLEAN``` |
| http_cookies.is_secure | ```IFF(RAW:data:request:cookie IS NOT NULL AND RAW:data:request:cookie ILIKE '%%secure;%%','true', 'false')::BOOLEAN``` |
| http_cookies.value | ```RAW:data:request:cookie::VARCHAR``` |
| http_request.http_method | ```CASE WHEN RAW:data:request:method = 'CONNECT' THEN 'CONNECT' WHEN RAW:data:request:method = 'DELETE' THEN 'DELETE' WHEN RAW:data:request:method = 'GET' THEN 'GET' WHEN RAW:data:request:method = 'HEAD' THEN 'HEAD' WHEN RAW:data:request:method = 'OPTIONS' THEN 'OPTIONS' WHEN RAW:data:request:method = 'POST' THEN 'POST' WHEN RAW:data:request:method = 'PUT' THEN 'PUT' WHEN RAW:data:request:method = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.uid | ```RAW:data:request:id::VARCHAR``` |
| http_request.url.path | ```SPLIT_PART(RAW:data:request:path, '?', 1)::VARCHAR``` |
| http_request.url.port | ```RAW:data:listenerPort::VARCHAR``` |
| http_request.url.query_string | ```SPLIT_PART(RAW:data:request:path, '?', 2)::VARCHAR``` |
| http_request.url.scheme | ```REGEXP_SUBSTR(RAW:data:request:httpVersion, '^([a-zA-Z]+)')::VARCHAR``` |
| http_request.url.url_string | ```RAW:data:request:path::VARCHAR``` |
| http_request.user_agent | ```RAW:data:request:agent::VARCHAR``` |
| http_request.version | ```REGEXP_SUBSTR(RAW:data:request:httpVersion, '([0-9\.]+)')::VARCHAR``` |
| http_response.code | ```RAW:data:response:code::NUMBER``` |
| http_response.content_type | ```RAW:data:response:contentType::VARCHAR``` |
| http_response.length | ```RAW:data:response:size::NUMBER``` |
| http_status | ```RAW:data:response:code::NUMBER``` |
| metadata.event_code | ```EVENT_TYPE``` |
| metadata.log_version | ```SPEC_VERSION::VARCHAR``` |
| metadata.product.name | ```'oracle-service-logs'``` |
| metadata.product.vendor_name | ```'oracle'``` |
| metadata.version | ```'1.1.0'``` |
| proxy_endpoint.hostname | ```RAW:data:host::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.ip | ```RAW:data:clientAddr::VARCHAR``` |
| src_endpoint.location.country | ```RAW:data:countryCode::VARCHAR``` |
| src_endpoint.name | ```SOURCE::VARCHAR``` |
| src_endpoint.port | ```RAW:data:listenerPort::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', INGESTED_TIME::VARCHAR::TIMESTAMP_LTZ)``` |
| start_time_dt | ```INGESTED_TIME::VARCHAR::TIMESTAMP_LTZ``` |
| status | ```CASE (CASE WHEN RAW:data:response:code ILIKE '2%%' THEN 1 WHEN RAW:data:response:code ILIKE '4%%' THEN 2 WHEN RAW:data:response:code ILIKE '5%%' THEN 2 WHEN RAW:data:response:code IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN RAW:data:response:code ILIKE '2%%' THEN 1 WHEN RAW:data:response:code ILIKE '4%%' THEN 2 WHEN RAW:data:response:code ILIKE '5%%' THEN 2 WHEN RAW:data:response:code IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', time::TIMESTAMP_LTZ)``` |
| time_dt | ```time::TIMESTAMP_LTZ``` |
| traffic.bytes_in | ```RAW:data:response:size::NUMBER``` |
| type_name | ```CASE (CASE WHEN RAW:data:request:method = 'CONNECT' THEN 400201 WHEN RAW:data:request:method = 'DELETE' THEN 400202 WHEN RAW:data:request:method = 'GET' THEN 400203 WHEN RAW:data:request:method = 'HEAD' THEN 400204 WHEN RAW:data:request:method = 'OPTIONS' THEN 400205 WHEN RAW:data:request:method = 'POST' THEN 400206 WHEN RAW:data:request:method = 'PUT' THEN 400207 WHEN RAW:data:request:method = 'TRACE' THEN 400208 WHEN RAW:data:request:method IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN RAW:data:request:method = 'CONNECT' THEN 400201 WHEN RAW:data:request:method = 'DELETE' THEN 400202 WHEN RAW:data:request:method = 'GET' THEN 400203 WHEN RAW:data:request:method = 'HEAD' THEN 400204 WHEN RAW:data:request:method = 'OPTIONS' THEN 400205 WHEN RAW:data:request:method = 'POST' THEN 400206 WHEN RAW:data:request:method = 'PUT' THEN 400207 WHEN RAW:data:request:method = 'TRACE' THEN 400208 WHEN RAW:data:request:method IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
