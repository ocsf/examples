# Event Dossier: Cato Networks Security Events to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `CatoNetworks`
* Product name: `cato-networks-security-events`
* Event codes: `All`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN ACTION is NULL then 0 WHEN ACTION = 'Allow' then 1 WHEN ACTION = 'Block' then 2 ELSE 99 END) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN ACTION is NULL then 0 WHEN ACTION = 'Allow' then 1 WHEN ACTION = 'Block' then 2 ELSE 99 END``` |
| activity_id | ```0::NUMBER``` |
| activity_name | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| app_name | ```APPLICATION::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```LOWER(IP_PROTOCOL)::VARCHAR``` |
| connection_info.protocol_num | ```CASE WHEN LOWER(IP_PROTOCOL) = 'icmp' THEN 1 WHEN LOWER(IP_PROTOCOL) = 'tcp' THEN 6 WHEN LOWER(IP_PROTOCOL) = 'udp' THEN 17 WHEN LOWER(IP_PROTOCOL) = 'rvd' THEN 66 WHEN LOWER(IP_PROTOCOL) = 'sun_nd' THEN 77 WHEN LOWER(IP_PROTOCOL) = 'ipv6' THEN 41 WHEN LOWER(IP_PROTOCOL) = 'mobile' THEN 55 WHEN LOWER(IP_PROTOCOL) = 'fire' THEN 125 END``` |
| count | ```EVENT_COUNT::NUMBER``` |
| device.os.type | ```CASE (CASE WHEN OS_TYPE = 'OS_WINDOWS' THEN 100 WHEN OS_TYPE = 'OS_UNKNOWN' THEN 0 WHEN OS_TYPE = 'OS_MAC' THEN 300 WHEN OS_TYPE = 'OS_LINUX' THEN 200 WHEN OS_TYPE = 'OS_IOS' THEN 301 WHEN OS_TYPE = 'OS_EMBEDDED' THEN 99 WHEN OS_TYPE = 'OS_ANDROID' THEN 201 END) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OS_TYPE = 'OS_WINDOWS' THEN 100 WHEN OS_TYPE = 'OS_UNKNOWN' THEN 0 WHEN OS_TYPE = 'OS_MAC' THEN 300 WHEN OS_TYPE = 'OS_LINUX' THEN 200 WHEN OS_TYPE = 'OS_IOS' THEN 301 WHEN OS_TYPE = 'OS_EMBEDDED' THEN 99 WHEN OS_TYPE = 'OS_ANDROID' THEN 201 END``` |
| device.region | ```DEST_SITE::VARCHAR``` |
| dst_endpoint.domain | ```DOMAIN_NAME::VARCHAR``` |
| dst_endpoint.ip | ```DEST_IP::VARCHAR``` |
| dst_endpoint.location.country | ```DEST_COUNTRY::VARCHAR``` |
| dst_endpoint.location.isp | ```ISP_NAME::VARCHAR``` |
| dst_endpoint.location.region | ```DEST_SITE::VARCHAR``` |
| dst_endpoint.port | ```DEST_PORT::VARCHAR``` |
| firewall_rule.desc | ```RULE_NAME::VARCHAR``` |
| firewall_rule.name | ```RULE::VARCHAR``` |
| firewall_rule.uid | ```RULE_ID::VARCHAR``` |
| metadata.event_code | ```event_sub_type``` |
| metadata.product.name | ```'cato-networks-security-events'``` |
| metadata.product.vendor_name | ```'CatoNetworks'``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.ip | ```SRC_IP::VARCHAR``` |
| src_endpoint.location.country | ```SRC_COUNTRY::VARCHAR``` |
| src_endpoint.location.region | ```SRC_SITE::VARCHAR``` |
| src_endpoint.port | ```SRC_PORT::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
