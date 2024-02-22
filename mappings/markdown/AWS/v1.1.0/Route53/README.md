# Event Dossier: Amazon Route53 Resolver Query Log
### NOERROR Query Results
- **Description**: Translates a Route53 Resolver query log to OCSF. 
- **Event References**:
  - https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html

 ### OCSF Version: 1.1.0
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4003`
 - `class_name`: `DNS Activity`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud, security_control, datetime]`
 - `metadata.product.name`: `Route 53`
 - `metadata.product.feature.name`: `Resolver Query Logs`
 - `metadata.product.vendor_name`: `AWS`
 - `severity`: `Informational`
 - `severity_id`: `1`
 - `activity_name`: `Traffic`
 - `activity_id`: `6`
 - `type_name`: `DNS Activity: Traffic`
 - `type_uid`: `400306`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any field not present in an explicit mapping will be moved to the unmapped object.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.product.version` | `version`       |
|`cloud.account.uid`|`account_id`|
|`cloud.region`|`region`|
|`src_endpoint.vpc_uid`|`vpc_id`|
|`time`|`query_timestamp`|
|`time_dt`|`query_timestamp`|
|`query.hostname`|`query_name`|
|`query.type`|`query_type`|
|`query.class`|`query_class`|
|`rcode`|`rcode`|
|`rcode_id`|`rcode`|
|`answers[].type`|`answers[].Type`|
|`answers[].rdata`|`answers[].Rdata`|
|`answers[].class`|`answers[].Class`|
|`src_endpoint.ip`|`srcaddr`|
|`src_endpoint.port`|`srcport`|
|`connection_info.protocol_name`|`transport`|
|`src_endpoint.instance_uid`|`srcids.instance`|
|`dst_endpoint.instance_uid`|`srcids.resolver_endpoint`|
|`dst_endpoint.interface_uid`|`srcids.resolver_network_interface`|
|`firewall_rule.uid`|`firewall_rule_group_id`|

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`action_id`|`firewall_rule_action`|
|`action`|`firewall_rule_action`|
|`disposition`|`firewall_rule_action`|

### Observables:

- All Hostnames, IP Addresses, EC2 Instance IDs will be populated as observables in each record. These will conform to the observable types mentioned described in [OCSF](https://schema.ocsf.io/1.1.0/objects/observable).