# Event Dossier: Amazon Route53 Query Log
### NOERROR Query Results
- **Description**: Translates a Route53 query log to OCSF. 
- **Event References**:
  - https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html

 ### OCSF Version: 0.33.0
 - `category_uid`: `4` `(Network Activity)`
 - `class_uid`: `4003` `(DNS Activity)`
 - `metadata.profiles`: `[cloud]`
 - `metadata.product.name`: `Route 53`
 - `metadata.product.feature.name`: `Query Logs`
 - `metadata.product.vendor_name`: `AWS`
 - `severity`: `Other`
 - `severity_id`: `-1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
| `metadata.product.version` | `version`       |
|`cloud.account_uid`|`account_id`|
|`cloud.region`|`region`|
|`src_endpoint.vpc_uid`|`vpc_id`|
|`time`|`query_timestamp`|
|`query.hostname`|`query_name`|
|`query.type`|`query_type`|
|`query.class`|`query_class`|
|`rcode`|`rcode`|
|`answers[].type`|`answers[].Type`|
|`answers[].rdata`|`answers[].Rdata`|
|`answers[].class`|`answers[].Class`|
|`src_endpoint.ip`|`srcaddr`|
|`src_endpoint.port`|`srcport`|
|`connection_info.protocol_name`|`transport`|
|`src_endpoint.instance_uid`|`srcids.instance`|
|`dst_endpoint.instance_uid`|`srcids.resolver_endpoint`|
|`dst_endpoint.interface_uid`|`srcids.resolver_network_interface`|
|`unmapped.firewall_rule_group_id`|`firewall_rule_group_id`|
|`unmapped.firewall_rule_action`|`firewall_rule_action`|
|`unmapped.firewall_domain_list_id`|`firewall_domain_list_id`|