# Event Dossier: Axis Activity Logs to OCSF class Dns Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `dns_activity`
* Vendor name: `axis`
* Product name: `axis-activity-logs`
* Event codes: `EVENT_TYPE = 'DnsRequest'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (CASE WHEN IS_BLOCKED='FALSE' THEN 1 WHEN IS_BLOCKED='TRUE' THEN 2 WHEN IS_BLOCKED IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```CASE WHEN IS_BLOCKED='FALSE' THEN 1 WHEN IS_BLOCKED='TRUE' THEN 2 WHEN IS_BLOCKED IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| activity_id | ```2::NUMBER``` |
| activity_name | ```CASE (2::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Query' WHEN 2 THEN 'Response' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.user.email_addr | ```USER_EMAIL::VARCHAR``` |
| actor.user.name | ```USERNAME::VARCHAR``` |
| actor.user.org.name | ```ORGANIZATION_NAME::VARCHAR``` |
| actor.user.org.uid | ```ORGANIZATION_ID::VARCHAR``` |
| actor.user.uid | ```USER_ID::VARCHAR``` |
| app_name | ```APP_NAME::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'dns_activity'``` |
| class_uid | ```4003``` |
| cloud.provider | ```IDENTITY_PROVIDER_NAME::VARCHAR``` |
| device.os.name | ```OPERATING_SYSTEM::VARCHAR``` |
| device.os.type | ```CASE (CASE WHEN OPERATING_SYSTEM='Windows' THEN 100 WHEN OPERATING_SYSTEM='Windows Mobile' THEN 101 WHEN OPERATING_SYSTEM='Linux' THEN 200 WHEN OPERATING_SYSTEM='Android' THEN 201 WHEN OPERATING_SYSTEM='Mac OS X' THEN 300 WHEN OPERATING_SYSTEM='iOS' THEN 301 WHEN OPERATING_SYSTEM='iPadOS' THEN 302 WHEN OPERATING_SYSTEM='Solaris' THEN 400 WHEN OPERATING_SYSTEM='AIX' THEN 401 WHEN OPERATING_SYSTEM='HP-UX' THEN 402 WHEN OPERATING_SYSTEM IS NULL THEN 0 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 100 THEN 'Windows' WHEN 101 THEN 'Windows Mobile' WHEN 200 THEN 'Linux' WHEN 201 THEN 'Android' WHEN 300 THEN 'macOS' WHEN 301 THEN 'iOS' WHEN 302 THEN 'iPadOS' WHEN 400 THEN 'Solaris' WHEN 401 THEN 'AIX' WHEN 402 THEN 'HP-UX' WHEN 99 THEN 'Other' END``` |
| device.os.type_id | ```CASE WHEN OPERATING_SYSTEM='Windows' THEN 100 WHEN OPERATING_SYSTEM='Windows Mobile' THEN 101 WHEN OPERATING_SYSTEM='Linux' THEN 200 WHEN OPERATING_SYSTEM='Android' THEN 201 WHEN OPERATING_SYSTEM='Mac OS X' THEN 300 WHEN OPERATING_SYSTEM='iOS' THEN 301 WHEN OPERATING_SYSTEM='iPadOS' THEN 302 WHEN OPERATING_SYSTEM='Solaris' THEN 400 WHEN OPERATING_SYSTEM='AIX' THEN 401 WHEN OPERATING_SYSTEM='HP-UX' THEN 402 WHEN OPERATING_SYSTEM IS NULL THEN 0 ELSE 99 END::NUMBER``` |
| firewall_rule.name | ```RULE_NAME::VARCHAR``` |
| firewall_rule.uid | ```RULE_ID::VARCHAR``` |
| metadata.product.name | ```'axis-activity-logs'``` |
| metadata.product.vendor_name | ```'axis'``` |
| metadata.version | ```'1.1.0'``` |
| query.hostname | ```HOST_NAME::VARCHAR``` |
| src_endpoint.ip | ```SOURCE_IP::VARCHAR``` |
| src_endpoint.location.country | ```GEOLOCATION::VARCHAR``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
