# Event Dossier: Bind Dns Logs to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `bind`
* Product name: `bind-dns-logs`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN RAW:block IS NULL THEN 0 WHEN RAW:block = false THEN 1 WHEN RAW:block = true THEN 2 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN RAW:block IS NULL THEN 0 WHEN RAW:block = false THEN 1 WHEN RAW:block = true THEN 2 ELSE 99 END::NUMBER``` |
| activity_id | ```CASE WHEN RAW:event:action IS NULL THEN 0 WHEN RAW:event:action = 'dns_query' THEN 1 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN RAW:event:action IS NULL THEN 0 WHEN RAW:event:action = 'dns_query' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.process.pid | ```RAW:pid::NUMBER``` |
| answers | ```ARRAY_CONSTRUCT(OBJECT_CONSTRUCT( 'flag_ids', ARRAY_CONSTRUCT(CASE WHEN HEADER_FLAGS[0] IS NULL THEN 0 WHEN HEADER_FLAGS[0] = 'AA' THEN 1 WHEN HEADER_FLAGS[0] = 'TC' THEN 2 WHEN HEADER_FLAGS[0] = 'RD' THEN 3 WHEN HEADER_FLAGS[0] = 'RA' THEN 4 WHEN HEADER_FLAGS[0] = 'AD' THEN 5 WHEN HEADER_FLAGS[0] = 'CD' THEN 6 ELSE 99 END), 'flags', ARRAY_CONSTRUCT(CASE (CASE WHEN HEADER_FLAGS[0] IS NULL THEN 0 WHEN HEADER_FLAGS[0] = 'AA' THEN 1 WHEN HEADER_FLAGS[0] = 'TC' THEN 2 WHEN HEADER_FLAGS[0] = 'RD' THEN 3 WHEN HEADER_FLAGS[0] = 'RA' THEN 4 WHEN HEADER_FLAGS[0] = 'AD' THEN 5 WHEN HEADER_FLAGS[0] = 'CD' THEN 6 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Authoritative Answer' WHEN 2 THEN 'Truncated Response' WHEN 3 THEN 'Recursion Desired' WHEN 4 THEN 'Recursion Available' WHEN 5 THEN 'Authentic Data' WHEN 6 THEN 'Checking Disabled' WHEN 99 THEN 'Other' END), 'ttl', RAW:answers[0]:ttl ))::ARRAY``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| connection_info.protocol_name | ```LOWER(NETWORK_PROTOCOL)::VARCHAR``` |
| connection_info.protocol_num | ```CASE WHEN NETWORK_PROTOCOL = 'TCP' THEN 6 WHEN NETWORK_PROTOCOL = 'UDP' THEN 17 ELSE -1 END::NUMBER``` |
| dst_endpoint.domain | ```RAW:dns:tld:domain::VARCHAR``` |
| dst_endpoint.hostname | ```RAW:host::VARCHAR``` |
| dst_endpoint.ip | ```DESTINATION_IP::VARCHAR``` |
| dst_endpoint.name | ```RAW:data_proc_endpoint::VARCHAR``` |
| dst_endpoint.port | ```DESTINATION_PORT::VARCHAR``` |
| dst_endpoint.uid | ```RAW:h_id::VARCHAR``` |
| metadata.product.name | ```'bind-dns-logs'``` |
| metadata.product.vendor_name | ```'bind'``` |
| metadata.version | ```'1.1.0'``` |
| query.hostname | ```QUERIED_ADDRESS::VARCHAR``` |
| query.type | ```RECORD_TYPE::VARCHAR``` |
| severity | ```CASE (CASE WHEN RAW:severityName IS NULL THEN 0 WHEN RAW:severityName = 'info' THEN 1 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Informational' WHEN 2 THEN 'Low' WHEN 3 THEN 'Medium' WHEN 4 THEN 'High' WHEN 5 THEN 'Critical' WHEN 6 THEN 'Fatal' WHEN 99 THEN 'Other' END``` |
| severity_id | ```CASE WHEN RAW:severityName IS NULL THEN 0 WHEN RAW:severityName = 'info' THEN 1 ELSE 99 END::NUMBER``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| src_endpoint.name | ```RAW:logsource::VARCHAR``` |
| src_endpoint.port | ```RAW:source:port::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| type_name | ```CASE ((400300 + (CASE WHEN RAW:event:action IS NULL THEN 0 WHEN RAW:event:action = 'dns_query' THEN 1 ELSE 99 END))::NUMBER) WHEN 400300 THEN 'DNS Activity: Unknown' WHEN 400301 THEN 'DNS Activity: Query' WHEN 400302 THEN 'DNS Activity: Response' WHEN 400306 THEN 'DNS Activity: Traffic' WHEN 400399 THEN 'DNS Activity: Other' END``` |
| type_uid | ```(400300 + (CASE WHEN RAW:event:action IS NULL THEN 0 WHEN RAW:event:action = 'dns_query' THEN 1 ELSE 99 END))::NUMBER``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
