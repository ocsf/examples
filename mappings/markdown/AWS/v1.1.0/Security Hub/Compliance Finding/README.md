# Event Dossier: Amazon Security Hub Finding
### Amazon Security Hub CSPM finding in ASFF format
- **Description**: Translates Amazon Security Hub CSPM finding in ASFF format to OCSF.
- **Event References**:
  - https://docs.aws.amazon.com/securityhub/latest/userguide/asff-required-attributes.html
  - https://docs.aws.amazon.com/securityhub/latest/userguide/asff-top-level-attributes.html

 ### OCSF Version: 1.1.0
 - `category_uid`: `2`
 - `category_name`: `Findings`
 - `class_uid`: `2002`
 - `class_name`: `Compliance Finding`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud, datetime]`
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
|`resources.type`|`Resources[].Type`|
|`resources.uid`|`Resources[].Id`|
|`resources.cloud_partition`|`Resources[].Partition`|
|`resources.region`|`Resources[].Region`|
|`resources.labels`|`Resources[].Tags`|
|`resources.data`|`Resources[].Details`|
|`resources.criticality`|`Criticality`|
|||
|`remediation.desc`|`Remediation.Recommendation.Text`|
|`remediation.references`|`Remediation.Recommendation.Url`|
|||
|`compliance.control`|`Compliance.SecurityControlId`|
|`compliance.status`|`Compliance.Status`|
|`compliance.requirements`|`Compliance.RelatedRequirements[]`|
|`compliance.status_detail`|`Compliance.StatusReasons[].Description`|
|`compliance.status_code`|`Compliance.StatusReasons[].ReasonCode`|
|`compliance.standards`|`Compliance.AssociatedStandards[].StandardsId`|

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


### Observables:

- All Hostnames, IP Addresses, Hashes, User Names, Resource ARNs, Process Names, will be populated as observables in each record. These will conform to the observable types described in [OCSF](https://schema.ocsf.io/1.1.0/objects/observable).
