# Event Dossier: Amazon EKS control plane Logging

### A generic EKS control plane event
- **Description**: A generic EKS control plane event to OCSF.
- **Event References**:
  - [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-examples.html](https://docs.aws.amazon.com/eks/latest/userguide/control-plane-logs.html)

 ### OCSF Version: 1.1.0
  - `class_name`: `API Activity`
  - `class_uid`: `6003`
  - `category_name`: `Application Activity`
  - `category_uid`: `6`
  - `cloud.provider`: `AWS`
  - `severity_id`: `1`
  - `severity`: `Informational`
  - `metadata.product.name`: `Amazon EKS`
  - `metadata.product.feature.name`: `Elastic Kubernetes Service`
  - `metadata.product.vendor_name`: `AWS`
  - `metadata.profiles`: `[cloud, datetime]`
  - `actor.user.type_id`: `0`

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
|`resources[].uid`|`objectRef.uid`|
|`resources[].version`|`objectRef.resourceVersion`|
|`api.version`|`objectRef.apiVersion`|
|`api.response.code`|`responseStatus.code`|
|`api.response.message`|`responseStatus.message`|
|`api.response.error`|`responseStatus.reason`|
|`api.response.error_message`|`responseStatus.status`|
|`api.group.name`|`objectRef.apiGroup`|
|`api.response.containers[].name`|`responseObject.spec.containers[].name`|
|`api.response.containers[].image.name`|`responseObject.spec.containers[].image`|
|`api.response.containers[].image.path`|`responseObject.spec.containers[].volumeMounts[].mountPath`|
|`api.response.containers[].image.uid`|`responseObject.spec.containers[].volumeMounts[].name`|
|`api.request.containers[].name`|`requestObject.spec.containers[].name`|
|`api.request.containers[].image.name`|`requestObject.spec.containers[].image`|
|`api.request.containers[].image.path`|`requestObject.spec.containers[].volumeMounts[].mountPath`|
|`api.request.containers[].image.uid`|`requestObject.spec.containers[].volumeMounts[].name`|
|`resources[].type`|`concat(objectRef.resource;objectRef.subresource)`|
|`start_time`|`requestReceivedTimestamp`|
|`time`|`stageTimestamp`|

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`activity_name`|`verb`|
|`activity_id`|`verb`|
|`type_uid`|`verb`|
|`type_name`|`verb`|
