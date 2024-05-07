# Event Dossier: Vectra Metadata Logs to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `vectra`
* Product name: `vectra-metadata-logs`
* Event codes: `METADATA_TYPE IN ('metadata_httpsessioninfo')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE WHEN RAW:method = 'CONNECT' THEN 1 WHEN RAW:method = 'DELETE' THEN 2 WHEN RAW:method = 'GET' THEN 3 WHEN RAW:method = 'HEAD' THEN 4 WHEN RAW:method = 'OPTIONS' THEN 5 WHEN RAW:method = 'POST' THEN 6 WHEN RAW:method = 'PUT' THEN 7 WHEN RAW:method = 'TRACE' THEN 8 WHEN RAW:method IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN RAW:method = 'CONNECT' THEN 1 WHEN RAW:method = 'DELETE' THEN 2 WHEN RAW:method = 'GET' THEN 3 WHEN RAW:method = 'HEAD' THEN 4 WHEN RAW:method = 'OPTIONS' THEN 5 WHEN RAW:method = 'POST' THEN 6 WHEN RAW:method = 'PUT' THEN 7 WHEN RAW:method = 'TRACE' THEN 8 WHEN RAW:method IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.session.uid | ```ORIG_SLUID::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (1::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```1::NUMBER``` |
| connection_info.protocol_ver | ```CASE (PARSE_IP(ID_ORIG_H, 'INET'):family::NUMBER) WHEN 0 THEN 'Unknown' WHEN 4 THEN 'Internet Protocol version 4 (IPv4)' WHEN 6 THEN 'Internet Protocol version 6 (IPv6)' WHEN 99 THEN 'Other' END``` |
| connection_info.protocol_ver_id | ```PARSE_IP(ID_ORIG_H, 'INET'):family::NUMBER``` |
| connection_info.session.uid | ```RESP_SLUID::VARCHAR``` |
| connection_info.uid | ```UID::VARCHAR``` |
| disposition | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 10 THEN 'Exonerated' WHEN 11 THEN 'Corrected' WHEN 12 THEN 'Partially Corrected' WHEN 13 THEN 'Uncorrected' WHEN 14 THEN 'Delayed' WHEN 15 THEN 'Detected' WHEN 16 THEN 'No Action' WHEN 17 THEN 'Logged' WHEN 18 THEN 'Tagged' WHEN 19 THEN 'Alert' WHEN 2 THEN 'Blocked' WHEN 20 THEN 'Count' WHEN 21 THEN 'Reset' WHEN 22 THEN 'Captcha' WHEN 23 THEN 'Challenge' WHEN 24 THEN 'Access Revoked' WHEN 25 THEN 'Rejected' WHEN 26 THEN 'Unauthorized' WHEN 27 THEN 'Error' WHEN 3 THEN 'Quarantined' WHEN 4 THEN 'Isolated' WHEN 5 THEN 'Deleted' WHEN 6 THEN 'Dropped' WHEN 7 THEN 'Custom Action' WHEN 8 THEN 'Approved' WHEN 9 THEN 'Restored' WHEN 99 THEN 'Other' END``` |
| disposition_id | ```0::NUMBER``` |
| dst_endpoint.hostname | ```RESP_HOSTNAME::VARCHAR``` |
| dst_endpoint.ip | ```ID_RESP_H::VARCHAR``` |
| dst_endpoint.port | ```RAW['id.resp_p']::VARCHAR``` |
| dst_endpoint.uid | ```RESP_HUID::VARCHAR``` |
| http_cookies.is_http_only | ```IFF(RAW:cookie IS NOT NULL AND RAW:cookie ILIKE '%%httponly;%%', 'true', 'false')::BOOLEAN``` |
| http_cookies.is_secure | ```IFF(RAW:cookie IS NOT NULL AND RAW:cookie ILIKE '%%secure;%%', 'true', 'false')::BOOLEAN``` |
| http_cookies.name | ```RAW:cookie_vars::VARCHAR``` |
| http_cookies.path | ```REGEXP_SUBSTR(RAW:cookie, '\\$Path=([^;]+)')::VARCHAR``` |
| http_cookies.value | ```RAW:cookie::VARCHAR``` |
| http_request.http_method | ```CASE WHEN RAW:method = 'CONNECT' THEN 'CONNECT' WHEN RAW:method = 'DELETE' THEN 'DELETE' WHEN RAW:method = 'GET' THEN 'GET' WHEN RAW:method = 'HEAD' THEN 'HEAD' WHEN RAW:method = 'OPTIONS' THEN 'OPTIONS' WHEN RAW:method = 'POST' THEN 'POST' WHEN RAW:method = 'PUT' THEN 'PUT' WHEN RAW:method = 'TRACE' THEN 'TRACE' ELSE NULL END::VARCHAR``` |
| http_request.length | ```RAW:request_body_len::NUMBER``` |
| http_request.referrer | ```RAW:referrer::VARCHAR``` |
| http_request.uid | ```ORIG_HUID::VARCHAR``` |
| http_request.url.hostname | ```RAW:host::VARCHAR``` |
| http_request.url.path | ```SPLIT_PART(REGEXP_REPLACE(RAW:uri, '^https?://[^/]+', ''), '?', 1)::VARCHAR``` |
| http_request.url.port | ```RAW['id.resp_p']::VARCHAR``` |
| http_request.url.query_string | ```SPLIT_PART(RAW:uri, '?', 2)::VARCHAR``` |
| http_request.url.scheme | ```REGEXP_SUBSTR(RAW:uri, '^([a-zA-Z]+)')::VARCHAR``` |
| http_request.url.url_string | ```RAW:uri::VARCHAR``` |
| http_request.user_agent | ```RAW:user_agent::VARCHAR``` |
| http_request.x_forwarded_for | ```RAW:proxied::VARCHAR``` |
| http_response.code | ```RAW:status_code::NUMBER``` |
| http_response.content_type | ```RAW:resp_mime_types::VARCHAR``` |
| http_response.length | ```RAW:response_body_len::NUMBER``` |
| http_response.status | ```RAW:status_msg::VARCHAR``` |
| http_status | ```RAW:status_code::NUMBER``` |
| metadata.event_code | ```METADATA_TYPE``` |
| metadata.product.name | ```'vectra-metadata-logs'``` |
| metadata.product.vendor_name | ```'vectra'``` |
| metadata.version | ```'1.1.0'``` |
| proxy.ip | ```REGEXP_SUBSTR(RAW:proxied, '([0-9]{1,3}\.){3}[0-9]{1,3}')::VARCHAR``` |
| severity | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```0::NUMBER``` |
| src_endpoint.hostname | ```RAW:orig_hostname::VARCHAR``` |
| src_endpoint.ip | ```ID_ORIG_H::VARCHAR``` |
| src_endpoint.port | ```ID_ORIG_P::VARCHAR``` |
| src_endpoint.uid | ```ORIG_HUID::VARCHAR``` |
| status | ```CASE (CASE WHEN RAW:status_code ILIKE '2%%' THEN 1 WHEN RAW:status_code ILIKE '4%%' THEN 2 WHEN RAW:status_code ILIKE '5%%' THEN 2 WHEN RAW:status_code IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_id | ```CASE WHEN RAW:status_code ILIKE '2%%' THEN 1 WHEN RAW:status_code ILIKE '4%%' THEN 2 WHEN RAW:status_code ILIKE '5%%' THEN 2 WHEN RAW:status_code IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| traffic.bytes | ```CAST(RAW:resp_ip_bytes AS NUMBER) + CAST(RAW:orig_ip_bytes AS NUMBER)::NUMBER``` |
| traffic.bytes_in | ```RAW:resp_ip_bytes::NUMBER``` |
| traffic.bytes_out | ```RAW:orig_ip_bytes::NUMBER``` |
| traffic.packets | ```CAST(RAW:resp_pkts AS NUMBER) + CAST(RAW:orig_pkts AS NUMBER)::NUMBER``` |
| traffic.packets_in | ```RAW:resp_pkts::NUMBER``` |
| traffic.packets_out | ```RAW:orig_pkts::NUMBER``` |
| type_name | ```CASE (CASE WHEN RAW:method = 'CONNECT' THEN 400201 WHEN RAW:method = 'DELETE' THEN 400202 WHEN RAW:method = 'GET' THEN 400203 WHEN RAW:method = 'HEAD' THEN 400204 WHEN RAW:method = 'OPTIONS' THEN   400205 WHEN RAW:method = 'POST' THEN 400206 WHEN RAW:method = 'PUT' THEN 400207 WHEN RAW:method = 'TRACE' THEN 400208 WHEN RAW:method IS NULL THEN 400200 ELSE 400299 END::NUMBER) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```CASE WHEN RAW:method = 'CONNECT' THEN 400201 WHEN RAW:method = 'DELETE' THEN 400202 WHEN RAW:method = 'GET' THEN 400203 WHEN RAW:method = 'HEAD' THEN 400204 WHEN RAW:method = 'OPTIONS' THEN   400205 WHEN RAW:method = 'POST' THEN 400206 WHEN RAW:method = 'PUT' THEN 400207 WHEN RAW:method = 'TRACE' THEN 400208 WHEN RAW:method IS NULL THEN 400200 ELSE 400299 END::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
