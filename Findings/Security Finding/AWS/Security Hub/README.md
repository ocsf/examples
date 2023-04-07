# Event Dossier: Amazon Security Hub Finding
### A Generic Security Hub finding in ASFF format
- **Description**: Translates a generic Amazon Security Hub Finding to OCSF.
- **Event References**:
  - https://docs.aws.amazon.com/securityhub/latest/userguide/asff-required-attributes.html
  - https://docs.aws.amazon.com/securityhub/latest/userguide/asff-top-level-attributes.html

 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `2`
 - `category_name`: `Findings`
 - `class_uid`: `2001`
 - `class_name`: `Security Finding`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud]`
 - `metadata.product.name`: `Security Hub`
 - `metadata.product.vendor_name`: `AWS`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements. 
 - Any field not present in an explicit mapping will be moved to the unmapped object.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.product.version` | `Schemaversion`       |
|`finding.uid`|`Id`|
|`metadata.product.uid`|`ProductArn`|
|`metadata.product.product.name`|`ProductName`|
|`metadata.product.product.feature.name`|`ProductName`|
|`metadata.product.vendor_name`|`CompanyName`|
|`cloud.region`|`Region`|
|`metadata.product.feature.uid`|`GeneratorId`|
|`cloud.account_uid`|`AwsAccountId`|
|`finding.types[]`|`Types[]`|
|`finding.first_seen_time`|`FirstObservedAt`|
|`finding.last_seen_time`|`LastObservedAt`|
|`time`|`LastObservedAt`|
|`finding.created_time`|`CreatedAt`|
|`finding.modified_time`|`UpdatedAt`|
|`severity`|`Severity.Label`|
|`finding.title`|`Title`|
|`finding.desc`|`Description`|
|`finding.remediation.desc`|`Remediation.Recommendation.Text`|
|`finding.remediation.kb_articles[]`|`Remediation.Recommendation.Url`|
|`finding.related_events[].product_uid`|`RelatedFindings[].ProductArn`|
|`finding.related_events[].uid`|`RelatedFindings[].Id`|
|`process.name`|`Process.name`|
|`process.file.path`|`Process.Path`|
|`process.pid`|`Process.Pid`|
|`process.parent_process.pid`|`Process.ParentPid`|
|`process.created_time`|`Process.LaunchedAt`|
|`process.terminated_time`|`Process.TerminatedAt`|
|`resources[].type`|`Resources[].Type`|
|`resources[].uid`|`Resources[].Id`|
|`resources[].cloud_partition`|`Resources[].Partition`|
|`resources[].region`|`Resources[].Region`|
|`resources[].labels`|`Resources[].Tags`|
|`resources[].details`|`Resources[].Details`|
|`compliance.status`|`Compliance.Status`|
|`compliance.requirements[]`|`Compliance.RelatedRequirements[]`|
|`compliance.status_detail`|`Compliance.StatusReasons[].Description`|
|`malware[].name`|`Malware[].Name`|
|`malware[].path`|`Malware[].Path`|
|`malware[].classifications[]`|`Malware[].Type`|
|`vulnerabilities[].cve.cvss.base_score`|`Vulnerabilities[].Cvss[].BaseScore`|
|`vulnerabilities[].cve.cvss.vector_string`|`Vulnerabilities[].Cvss[].BaseVector`|
|`vulnerabilities[].cve.cvss.version`|`Vulnerabilities[].Cvss[].Version`|
|`vulnerabilities[].cve.uid`|`Vulnerabilities[].Cvss[].Id`|
|`vulnerabilities[].cve.created_time`|`Vulnerabilities[].Vendor.VendorCreatedAt`|
|`vulnerabilities[].cve.modified_time`|`Vulnerabilities[].Vendor.VendorUpdatedAt`|
|`vulnerabilities[].references[]`|`Vulnerabilities[].ReferenceUrls[]`|
|`vulnerabilities[].related_vulnerabilities[]`|`Vulnerabilities[].RelatedVulnerabilities[]`|
|`vulnerabilities[].vendor_name`|`Vulnerabilities[].Vendor.Name`|
|`vulnerabilities[].Vendor.kb_articles[]`|`Vulnerabilities[].Vendor.Url`|
|`vulnerabilities[].packages[].architecture`|`Vulnerabilities[].VulnerablePackages[].Architecture`|
|`vulnerabilities[].packages[].epoch`|`Vulnerabilities[].VulnerablePackages[].Epoch`|
|`vulnerabilities[].packages[].name`|`Vulnerabilities[].VulnerablePackages[].Name`|
|`vulnerabilities[].packages[].release`|`Vulnerabilities[].VulnerablePackages[].Release`|
|`vulnerabilities[].packages[].version`|`Vulnerabilities[].VulnerablePackages[].Version`|

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are are subject to dynamic mappings contingent on matching a condition within the mapping schema. Fields which fail to meet a particuclar conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`state`|`Workflow.Status`|
|`state_id`|`Workflow.Status`|
|`activity_name`|`CreatedAt/UpdatedAt`|
|`activity_id`|`CreatedAt/UpdatedAt`|
|`type_uid`|`CreatedAt/UpdatedAt`|
|`type_name`|`CreatedAt/UpdatedAt`|
