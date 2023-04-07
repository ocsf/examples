# Event Dossier: Amazon VPC Flowlogs
### Amazon VPC Flowlog Connection Refused
- **Description**: Translates Amazon VPC Flowlog event where a connection was refused to OCSF. The source might be in csv or parquet. The source field names may vary with a `-` compared to a `_` depending on the source type. This file has been anonymized and contains only 1 record showing version 5 fields in alphabetical order.
- **Event References**:
  - https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html

 ### OCSF Version: 0.99.2
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4001`
 - `class_name`: `Network Activity`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud, security_control]`
 - `metadata.product.name`: `Amazon VPC`
 - `metadata.product.feature.name`: `Flowlogs`
 - `metadata.product.vendor_name`: `AWS`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
| `metadata.product.version` | `version`       |
| `cloud.account_uid`        | `account_id`    |
| `cloud.region`             | `region`        |
|`cloud.zone`|`az_id`|
|`src_endpoint.port`|`srcport`|
|`dst_endpoint.port`|`dstport`|
|`connection_info.protocol_num`|`protocol`|
|`traffic.packets`|`packets`|
|`traffic.bytes`|`bytes`|
|`time`|`start`|
|`start_time`|`start`|
|`end_time`|`end`|
|`connection_info.tcp_flags`|`tcp_flags`|
|`connection_info.protocol_ver`|`protocol_ver`|
|`src_endpoint.svc_name`|`pkt_src_aws_service`|
|`dst_endpoint.svc_name`|`pkt_dst_aws_service`|
|`connection_info.direction`|`flow_direction`|
|`connection_info.direction_id`|`flow_direction`|
|`unmapped.sublocation_type`|`sublocation_type`|
|`unmapped.sublocation_id`|`sublocation_id`|
|`unmapped.sublocation_id`|`flow_direction`|
|`activity_name`|`action`|
|`activity_id`|`action`|
|`type_uid`|`action`|
|`type_name`|`action`|
|`disposition`|`action`|
|`disposition_id`|`action`|
|`status_code`|`log_status`|
|`connection_info.boundary_id`|`traffic_path`|
|`connection_info.boundary`|`traffic_path`|
|`connection_info.direction_id`|`flow_direction`|
|`dst_endpoint.intermediate_ips`|`pkt_dstaddr` or `dstaddr`|
|`dst_endpoint.ip`|`pkt_dstaddr` or `dstaddr`|
|`src_endpoint.intermediate_ips`|`pkt_srcaddr` or `srcaddr`|
|`src_endpoint.ip`|`pkt_srcaddr` or `srcaddr`|
|`dst_endpoint.interface_uid`|`interface_id`|
|`dst_endpoint.vpc_uid`|`vpc_id`|
|`dst_endpoint.instance_uid`|`instance_id`|
|`dst_endpoint.subnet_uid`|`subnet_id`|
|`src_endpoint.interface_uid`|`interface_id`|
|`src_endpoint.vpc_uid`|`vpc_id`|
|`src_endpoint.instance_uid`|`instance_id`|
|`src_endpoint.subnet_uid`|`subnet_id`|
