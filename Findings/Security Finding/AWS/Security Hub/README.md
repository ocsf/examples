# Event Dossier: Amazon Security Hub Findings Log
### NOERROR Query Results
- **Description**: Translates a Amazon Security Hub Finding log to OCSF. 

 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `2`
 - `category_name`: `Findings`
 - `class_uid`: `2001`
 - `class_name`: `Security Finding`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud]`
 - `metadata.product.name`: `Security Hub`
 - `metadata.product.feature.name`: `Security Hub`
 - `metadata.product.vendor_name`: `AWS`
 - `severity_id`: `1`
 - `type_uid`: `200102`
 - `type_name`: `Security Finding: Update`
 - `severity_id`: `1`
 - `activity_name`: `Update`
 - `activity_id`: `2`
 - `malware[].classification_ids`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.product.version` | `Schemaversion`       |
|`finding.uid`|`Id`|
|`state`|`Workflow.Status`|
|`state_id`|`Workflow.Status`|
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
|`finding.create_time`|`CreatedAt`|
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
|`resources[].labels.billingCode`|`Resources[].Tags.billingCode`|
|`resources[].labels.needsPatching`|`Resources[].Tags.needsPatching`|
|`resources[].details.Resources[].Details.AwsEc2SecurityGroup.GroupName`|`Resources[].Details.AwsEc2SecurityGroup.GroupName`|
|`resources[].details.AwsEc2SecurityGroup.GroupId`|`Resources[].Details.AwsEc2SecurityGroup.GroupId`|
|`resources[].details.AwsEc2SecurityGroup.OwnerId`|`Resources[].Details.AwsEc2SecurityGroup.OwnerId`|
|`resources[].details..AwsEc2SecurityGroup.VpcId`|`Resources[].Details.AwsEc2SecurityGroup.VpcId`|
|`resources[].details.AwsEc2SecurityGroup.IpPermissions[].IpProtocol`|`Resources[].Details.AwsEc2SecurityGroup.IpPermissions[].IpProtocol`|
|`resources[].details.AwsEc2SecurityGroup.IpPermissions[].UserIdGroupPairs[].GroupId`|`Resources[].Details.AwsEc2SecurityGroup.IpPermissions[].UserIdGroupPairs[].GroupId`|
|`resources[].details.AwsEc2SecurityGroup.IpPermissions[].UserIdGroupPairs[].UserId`|`Resources[].Details.AwsEc2SecurityGroup.IpPermissions[].UserIdGroupPairs[].UserId`|
|`resources[].details.AwsEc2SecurityGroup.IpPermissionsEgress[].IpProtocol`|`Resources[].Details.AwsEc2SecurityGroup.IpPermissionsEgress[].IpProtocol`|
|`resources[].details.AwsEc2SecurityGroup.IpPermissionsEgress[].IpRanges[].CidrIp`|`Resources[].Details.AwsEc2SecurityGroup.IpPermissionsEgress[].IpRanges[].CidrIp`|
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
