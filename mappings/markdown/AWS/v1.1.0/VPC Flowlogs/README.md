# Event Dossier: Amazon VPC Flowlogs
### Amazon VPC Flowlog Connection Refused
- **Description**: Translates Amazon VPC Flowlog event where a connection was refused to OCSF. The source might be in csv or parquet. The source field names may vary with a `-` compared to a `_` depending on the source type. This file has been anonymized and contains only 1 record showing version 5 fields in alphabetical order.
- **Event References**:
  - https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html

 ### OCSF Version: 1.1.0
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4001`
 - `class_name`: `Network Activity`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud, security_control, datetime]`
 - `metadata.product.name`: `Amazon VPC`
 - `metadata.product.feature.name`: `Flowlogs`
 - `metadata.product.vendor_name`: `AWS`
 - `metadata.version`: `1.1.0`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.product.version`|`version`|
|`cloud.account.uid`|`account_id`    |
|`cloud.region`| `region`|
|`cloud.zone`|`az_id`|
|`src_endpoint.port`|`srcport`|
|`dst_endpoint.port`|`dstport`|
|`connection_info.protocol_num`|`protocol`|
|`traffic.packets`|`packets`|
|`traffic.bytes`|`bytes`|
|`time`|`start`|
|`time_dt`|`start`|
|`start_time_dt`|`start`|
|`end_time_dt`|`end`|
|`connection_info.tcp_flags`|`tcp_flags`|
|`connection_info.protocol_ver`|`protocol_ver`|
|`src_endpoint.svc_name`|`pkt_src_aws_service`|
|`dst_endpoint.svc_name`|`pkt_dst_aws_service`|
|`status_code`|`log_status`|

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             | Notes             |
| -------------------------- | ----------------| ------------------|
|`activity_name`|`action`|
|`activity_id`|`action`|
|`type_uid`|`action`|
|`type_name`|`action`|
|`action`|`action`|
|`action_id`|`action`|
|`disposition`|`action`|
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

### Observables:

- All IP Addresses, EC2 Instance IDs will be populated as observables in each record. These will conform to the observable types mentioned described in [OCSF](https://schema.ocsf.io/1.1.0/objects/observable).