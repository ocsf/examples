# Event Dossier: Amazon WAF
### Amazon WAF Connection Refused
- **Description**: Translates Amazon WAF event where a connection was refused to OCSF. The source might be in csv or parquet. The source field names may vary with a `-` compared to a `_` depending on the source type. This file has been anonymized and contains only 1 record showing version 5 fields in alphabetical order.
- **Event References**:
  - https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html

 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4002`
 - `class_name`: `HTTP Activity`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud, firewall]`
 - `metadata.product.name`: `Amazon WAF`
 - `metadata.product.feature.name`: `WAF`
 - `metadata.product.vendor_name`: `AWS`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`webaclId`|`metadata.product.feature.uid`|
|`formatVersion`|`metadata.product.version`|
|`labels[]`| `metadata.labels[]`|
|`httpSourceName`|`src_endpoint.svc_name`|
|`httpSourceId`|`src_endpoint.uid`|
|`httpRequest.clientIp`|`src_endpoint.ip`|
|`httpRequest.country`|`src_endpoint.location.country`|
|`httpRequest.uri`|`http_request.url.path`|
|`httpRequest.uri`|`dst_endpoint.domain`|
|`httpRequest.httpVersion`|`http_request.version`|
|`httpRequest.httpMethod`|`http_request.http_method`|
|`httpRequest.requestId`|`http_request.uid`|
|`terminatingRuleId`|`firewall_rule.uid`|
|`terminatingRuleType`|`firewall_rule.type`|
|`httpRequest.args`|`http_request.args`|
|`terminatingRuleMatchDetails[].conditionType`|`firewall_rule.condition`|
|`terminatingRuleMatchDetails[].location`|`firewall_rule.match_location`|
|`terminatingRuleMatchDetails[].matchedData[]`|`firewall_rule.match_details[]`|
|`rateBasedRuleList[].maxRateAllowed`|`firewall_rule.rate_limit`|
|`requestHeadersInserted[].name`|`http_request.http_headers[].name`|
|`requestHeadersInserted[].value`|`http_request.http_headers[].value`|
|`responseCodeSent`|`firewall_rule.status_code`|
|`timestamp`|`time`|



 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             | Notes             |
| -------------------------- | ----------------| ------------------|
|`activity_name`|`action`|
|`activity_id`|`action`|
|`type_uid`|`action`|
|`type_name`|`action`|
|`disposition`|`action`|
|`disposition_id`|`action`|
|`connection_info.boundary_id`|`traffic_path`|
|`connection_info.boundary`|`traffic_path`|
|`connection_info.direction`|`flow_direction`|
|`connection_info.direction_id`|`flow_direction`|
|Subject to evaluation, _if `pkt_dstaddr` equals `dstaddr`_ - |
|`dst_endpoint.ip`|`dstaddr`| 
|_else_|
|`dst_endpoint.ip`|`pkt_dstaddr`|
|`dst_endpoint.intermediate_ips`|`dstaddr`|
|Subject to evaluation, _if `pkt_srcaddr` equals `srcaddr`_ - |
|`src_endpoint.ip`|`srcaddr`|
|_else_|
|`src_endpoint.ip`|`pkt_srcaddr`| 
|`src_endpoint.intermediate_ips`|`srcaddr`|
|Subject to evaluation, _if `flow_direction` equals `ingress`_ - |
|`dst_endpoint.interface_uid`|`interface_id`|
|`dst_endpoint.vpc_uid`|`vpc_id`|
|`dst_endpoint.instance_uid`|`instance_id`|
|`dst_endpoint.subnet_uid`|`subnet_id`|
|Subject to evaluation, _if `flow_direction` equals `egress`_ - |
|`src_endpoint.interface_uid`|`interface_id`|
|`src_endpoint.vpc_uid`|`vpc_id`|
|`src_endpoint.instance_uid`|`instance_id`|
|`src_endpoint.subnet_uid`|`subnet_id`|
