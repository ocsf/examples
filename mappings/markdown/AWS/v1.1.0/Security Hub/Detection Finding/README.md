# Event Dossier: Amazon Security Hub Finding
### Amazon GuardDuty finding in Security Hub's ASFF format
- **Description**: Translates Amazon GuardDuty finding in Security Hub's ASFF format to OCSF.
- **Event References**:
  - https://docs.aws.amazon.com/securityhub/latest/userguide/asff-required-attributes.html
  - https://docs.aws.amazon.com/securityhub/latest/userguide/asff-top-level-attributes.html

 ### OCSF Version: 1.1.0
 - `category_uid`: `2`
 - `category_name`: `Findings`
 - `class_uid`: `2004`
 - `class_name`: `Detection Finding`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud, datetime, linux]`
 - `metadata.extensions[].name`: `linux`
 - `metadata.extensions[].uid`: `1`
 - `metadata.extensions[].version`: `1.1.0`
 - `metadata.version`: `1.1.0`
 - `metadata.product.vendor_name`: `AWS`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any field not present in an explicit mapping will be moved to the unmapped object.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.log_version`|`Schemaversion`|
|`metadata.product.name`|`ProductName`|
|`metadata.product.uid`|`ProductArn`|
|`metadata.product.eature.name`|`ProductFields.aws/guardduty/service/featureName`|
|`metadata.product.vendor_name`|`CompanyName`|
|`metadata.product.feature.uid`|`GeneratorId`|
|`metadata.processed_time_dt`|`ProcessedAt`|
|||
|`cloud.region`|`Region`|
|`cloud.account.uid`|`AwsAccountId`|
|||
|`confidence_score`|`Confidence`|
|||
|`time`|`LastObservedAt`|
|`time_dt`|`LastObservedAt`|
|||
|`finding_info.uid`|`Id`|
|`finding_info.src_url`|`SourceUrl`|
|`finding_info.types[]`|`Types[]`|
|`finding_info.first_seen_time_dt`|`FirstObservedAt`|
|`finding_info.last_seen_time_dt`|`LastObservedAt`||
|`finding_info.created_time_dt`|`CreatedAt`|
|`finding_info.modified_time_dt`|`UpdatedAt`|
|`finding_info.title`|`Title`|
|`finding_info.desc`|`Description`|
|`finding_info.related_events[].product_uid`|`RelatedFindings[].ProductArn`|
|`finding_info.related_events[].uid`|`RelatedFindings[].Id`|
|||
|`message`|`Note.Text`|
|||
|`resources[].type`|`Resources[].Type`|
|`resources[].uid`|`Resources[].Id`|
|`resources[].cloud_partition`|`Resources[].Partition`|
|`resources[].region`|`Resources[].Region`|
|`resources[].labels`|`Resources[].Tags`|
|`resources[].data`|`Resources[].Details`|
|`resources[].criticality`|`Criticality`|
|`resources[].owner.account.uid`|`ProductFields.ResourceOwnerAccount`|
|||
|`evidences[].data`|`ProductFields.aws/guardduty/service/additionalInfo/value`|

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             | Notes |
| -------------------------- | ----------------| ------|
|`severity`|`Severity.Label`|
|`severity_id`|`Severity.Label`|
|`status`|`Workflow.Status`|
|`activity_name`|`CreatedAt/UpdatedAt`| Create, Update is determined based on finding timestamps|
|`activity_id`|`CreatedAt/UpdatedAt`| ^ |
|`type_uid`|`CreatedAt/UpdatedAt`| ^ |
|`type_name`|`CreatedAt/UpdatedAt`| ^ |
|||
|`evidences[].actor.process.name`|`ProductFields.aws/guardduty/service/runtimeDetails/process/name`|
|`evidences[].actor.process.file.path`|`ProductFields.aws/guardduty/service/runtimeDetails/process/executablePath`|
|`evidences[].actor.process.pid`|`ProductFields.aws/guardduty/service/runtimeDetails/process/pid`|
|`evidences[].actor.process.uid`|`ProductFields.aws/guardduty/service/runtimeDetails/process/uuid`|
|`evidences[].actor.process.created_time_dt`|`ProductFields.aws/guardduty/service/runtimeDetails/process/startTime`|
|`evidences[].actor.process.user.name`|`ProductFields.aws/guardduty/service/runtimeDetails/process/user`|
|`evidences[].actor.process.user.uid`|`ProductFields.aws/guardduty/service/runtimeDetails/process/userId`|
|`evidences[].actor.process.parent_process.uid`|`ProductFields.aws/guardduty/service/runtimeDetails/process/parentUuid`|
|`evidences[].actor.process.file.hashes[].value`|`ProductFields.aws/guardduty/service/runtimeDetails/process/executableSha256`|
|`evidences[].actor.process.euid`|`ProductFields.aws/guardduty/service/runtimeDetails/process/euid`|
|||
|`evidences[].process.name`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/name`|
|`evidences[].process.file.path`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/executablePath`|
|`evidences[].process.pid`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/pid`|
|`evidences[].process.uid`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/uuid`|
|`evidences[].process.created_time_dt`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/startTime`|
|`evidences[].process.user.name`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/user`|
|`evidences[].process.user.uid`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/userId`|
|`evidences[].process.parent_process.uid`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/parentUuid`|
|`evidences[].process.file.hashes[].value`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/executableSha256`|
|`evidences[].process.euid`|`ProductFields.aws/guardduty/service/runtimeDetails/context/targetProcess/euid`|
|||
|`evidences[].api.operation`|`ProductFields.aws/guardduty/service/awsApiCallAction/api`|
|`evidences[].api.operation`|`ProductFields.aws/guardduty/service/action/kubernetesApiCallAction/verb`|
|`evidences[].api.response.error`|`ProductFields.aws/guardduty/service/awsApiCallAction/errorCode`|
|`evidences[].api.service.name`|`ProductFields.aws/guardduty/service/awsApiCallAction/serviceName`|
|||
|`evidences[].src_endpoint.ip`|`ProductFields.aws/guardduty/service/awsApiCallAction/remoteIpDetails/ipAddressV4`|
|`evidences[].src_endpoint.ip`|`ProductFields.aws/guardduty/service/action/kubernetesApiCallAction/remoteIpDetails/ipAddressV4`|
|`evidences[].src_endpoint.location.country`|`ProductFields.aws/guardduty/service/awsApiCallAction/remoteIpDetails/country/countryName`|
|`evidences[].src_endpoint.location.country`|`ProductFields.aws/guardduty/service/action/kubernetesApiCallAction/remoteIpDetails/country/countryName`|
|`evidences[].src_endpoint.location.city`|`ProductFields.aws/guardduty/service/awsApiCallAction/remoteIpDetails/city/cityName`|
|`evidences[].src_endpoint.location.city`|`ProductFields.aws/guardduty/service/action/kubernetesApiCallAction/remoteIpDetails/city/cityName`|
|`evidences[].src_endpoint.location.coordinates[]`|`ProductFields.aws/guardduty/service/awsApiCallAction/remoteIpDetails/geoLocation/lon;ProductFields.aws/guardduty/service/awsApiCallAction/remoteIpDetails/geoLocation/lat`|
|`evidences[].src_endpoint.location.coordinates[]`|`ProductFields.aws/guardduty/service/action/kubernetesApiCallAction/remoteIpDetails/geoLocation/lon;ProductFields.aws/guardduty/service/action/kubernetesApiCallAction/remoteIpDetails/geoLocation/lat`|
|||
|`evidences[].query.hostname`|`ProductFields.aws/guardduty/service/action/dnsRequestAction/domainWithSuffix`|
|`evidences[].connection_info.protocol_name`|`ProductFields.aws/guardduty/service/action/dnsRequestAction/protocol`|


### Observables:

- All Hostnames, IP Addresses, Hashes, User Names, Resource ARNs, Process Names, will be populated as observables in each record. These will conform to the observable types described in [OCSF](https://schema.ocsf.io/1.1.0/objects/observable).
