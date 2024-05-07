# Event Dossier: Zscaler Zia to OCSF class Http Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `http_activity`
* Vendor name: `zscaler`
* Product name: `zscaler-zia`
* Event codes: `protocol in ('HTTP', 'HTTPS')`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION = 'Allowed' THEN 1 WHEN ACTION = 'Blocked' THEN 2 WHEN ACTION is not null THEN 99 ELSE 0 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION = 'Allowed' THEN 1 WHEN ACTION = 'Blocked' THEN 2 WHEN ACTION is not null THEN 99 ELSE 0 END``` |
| activity_id | ```CASE WHEN REQUEST_METHOD is null THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END``` |
| activity_name | ```CASE (CASE WHEN REQUEST_METHOD is null THEN 0 WHEN REQUEST_METHOD = 'CONNECT' THEN 1 WHEN REQUEST_METHOD = 'DELETE' THEN 2 WHEN REQUEST_METHOD = 'GET' THEN 3 WHEN REQUEST_METHOD = 'HEAD' THEN 4 WHEN REQUEST_METHOD = 'OPTIONS' THEN 5 WHEN REQUEST_METHOD = 'POST' THEN 6 WHEN REQUEST_METHOD = 'PUT' THEN 7 WHEN REQUEST_METHOD = 'TRACE' THEN 8 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Connect' WHEN 2 THEN 'Delete' WHEN 3 THEN 'Get' WHEN 4 THEN 'Head' WHEN 5 THEN 'Options' WHEN 6 THEN 'Post' WHEN 7 THEN 'Put' WHEN 8 THEN 'Trace' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```USER::VARCHAR``` |
| actor.user.name | ```USER::VARCHAR``` |
| api.operation | ```REQUEST_METHOD::VARCHAR``` |
| api.request.uid | ```EVENT_ID::VARCHAR``` |
| api.response.code | ```STATUS::NUMBER``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'http_activity'``` |
| class_uid | ```4002``` |
| connection_info.direction | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Inbound' WHEN 2 THEN 'Outbound' WHEN 3 THEN 'Lateral' WHEN 99 THEN 'Other' END``` |
| connection_info.direction_id | ```2::NUMBER``` |
| device.hostname | ```DEVICE_HOSTNAME::VARCHAR``` |
| device.ip | ```CLIENT_IP::VARCHAR``` |
| dst_endpoint.hostname | ```HOSTNAME::VARCHAR``` |
| dst_endpoint.ip | ```SERVER_IP::VARCHAR``` |
| http_request.http_method | ```REQUEST_METHOD::VARCHAR``` |
| http_request.length | ```REQUEST_SIZE::NUMBER``` |
| http_request.referrer | ```REFERER_URL::VARCHAR``` |
| http_request.uid | ```EVENT_ID::VARCHAR``` |
| http_request.url.hostname | ```HOSTNAME::VARCHAR``` |
| http_request.url.path | ```iff(TRIM(TRIM(URL,HOSTNAME),':443') = '',null,TRIM(TRIM(URL,HOSTNAME),':443'))::VARCHAR``` |
| http_request.url.port | ```CASE WHEN contains(url,':443') THEN 443::VARCHAR END``` |
| http_request.url.query_string | ```iff(contains(url,'?'), SPLIT_PART(url,'?',-1)::VARCHAR,null)``` |
| http_request.url.url_string | ```URL::VARCHAR``` |
| http_request.user_agent | ```USER_AGENT::VARCHAR``` |
| http_request.version | ```REQUEST_VERSION::VARCHAR``` |
| http_response.code | ```STATUS::NUMBER``` |
| http_response.content_type | ```CONTENT_TYPE::VARCHAR``` |
| metadata.product.name | ```'zscaler-zia'``` |
| metadata.product.vendor_name | ```'zscaler'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.hostname | ```DEVICE_HOSTNAME::VARCHAR``` |
| src_endpoint.ip | ```CLIENT_IP::VARCHAR``` |
| src_endpoint.name | ```DEVICE_HOSTNAME::VARCHAR``` |
| status | ```CASE (99::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Success' WHEN 2 THEN 'Failure' WHEN 99 THEN 'Other' END``` |
| status_detail | ```REASON::VARCHAR``` |
| status_id | ```99::NUMBER``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| traffic.bytes | ```RESPONSE_SIZE::NUMBER``` |
| traffic.bytes_in | ```RESPONSE_SIZE::NUMBER``` |
| traffic.bytes_out | ```REQUEST_SIZE::NUMBER``` |
| type_name | ```CASE (decode(REQUEST_METHOD, null, 400200, 'CONNECT' , 400201, 'DELETE',400202, 'GET',400203,'HEAD',400204,'OPTIONS',400205,'POST',400206,'PUT',400207,'TRACE',400208,400299)) WHEN 400200 THEN 'HTTP Activity: Unknown' WHEN 400201 THEN 'HTTP Activity: Connect' WHEN 400202 THEN 'HTTP Activity: Delete' WHEN 400203 THEN 'HTTP Activity: Get' WHEN 400204 THEN 'HTTP Activity: Head' WHEN 400205 THEN 'HTTP Activity: Options' WHEN 400206 THEN 'HTTP Activity: Post' WHEN 400207 THEN 'HTTP Activity: Put' WHEN 400208 THEN 'HTTP Activity: Trace' WHEN 400299 THEN 'HTTP Activity: Other' END``` |
| type_uid | ```decode(REQUEST_METHOD, null, 400200, 'CONNECT' , 400201, 'DELETE',400202, 'GET',400203,'HEAD',400204,'OPTIONS',400205,'POST',400206,'PUT',400207,'TRACE',400208,400299)``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
