# Event Dossier: Amazon EKS control plane Logging

### A generic EKS control plane event
- **Description**: A generic EKS control plane event to OCSF.
- **Event References**:
  - [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-examples.html](https://docs.aws.amazon.com/eks/latest/userguide/control-plane-logs.html)

 ### OCSF Version: 1.1.0-dev
  - `class_name`: `API Activity`
  - `class_uid`: `6003`
  - `category_name`: `Application Activity`
  - `category_uid`: `6`
  - `cloud.provider`: `AWS`
  - `severity_id`: `1`
  - `severity`: `Informational`
  - `metadata.product.name`: `AWS EKS`
  - `metadata.product.vendor_name`: `AWS`
  - `metadata.profiles`: `[cloud]`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.log_level`|`level`|
|`metadata.product.version`|`apiVersion`|
|`api.request.uid`|`auditID`|
|`message`|`stage`|
|`http_request.url.path`|`requestURI`|
|`api.operation`|`verb`|
|`actor.user.name`|`user.username`|
|`actor.user.uid`|`user.uid`|
|`actor.user.groups[].name`|`user.groups[]`|
|`actor.session.credential_uid`|`user.extra.accessKeyId[]`|
|`actor.session.uid`|`user.extra.sessionName[]`|
|`cloud.account.uid`|`sourceIPs[0]`|
|`src_endpoint.intermediate_ips[]`|`sourceIPs[:1]`|
|`http_request.user_agent`|`userAgent`|
|`resources[].namespace`|`objectRef.namespace`|
|`resources[].name`|`objectRef.name`|

|`api.operation`|`eventName`|
|`cloud.region`|`awsRegion`|
|`http_request.user_agent`|`userAgent`|
|`metadata.product.version`|`eventVersion`|
|`metadata.uid`|`eventID`|
|`metadata.version`|`eventVersion`|
|`time`|`eventTime`|
|`api.response.error`|`errorCode`|
|`api.response.message`|`errorMessage`|
|`resources[].uid`|`resources[].ARN`|
|`resources[].account_uid`|`resources[].accountId`|
|`resources[].type`|`resources[].type`|

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`status`|`errorCode`|
|`status_id`|`errorCode`|
|`metadata.product.feature.name`|`eventCategory`|
|`api.request.uid`|`requestID`|
|`src_endpoint.ip/src_endpoint.domain`|`sourceIPAddress`|
|`activity_name`|`eventName`|
|`activity_id`|`eventName`|
|`type_uid`|`eventName`|
|`type_name`|`eventName`|
