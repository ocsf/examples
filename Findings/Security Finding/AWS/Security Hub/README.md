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
 - `state_id`: `3`
 - `state`: `Suppressed`
 - `malware[].classification_ids`: `1`
 - 
 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

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
|`finding.create_time`|`CreatedAt`|
|`finding.modified_time`|`UpdatedAt`|
|`severity`|`Severity.Label`|
|`unmapped.Severity_Original`|`Severity.Original`|
|`unmapped.Severity_Normalized`|`Severity.Normalized`|
|`unmapped.Severity_Product`|`Severity.Product`|
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
|`unmapped.ProductFields.StandardsArn`|`ProductFields.StandardsArn`|
|`unmapped.ProductFields.StandardsSubscriptionArn`|`ProductFields.StandardsSubscriptionArn`|
|`unmapped.ProductFields.ControlId`|`ProductFields.ControlId`|
|`unmapped.ProductFields.RecommendationUrl`|`ProductFields.RecommendationUrl`|
|`unmapped.ProductFields.RelatedAWSResources:0/name`|`ProductFields.RelatedAWSResources:0/name`|
|`unmapped.ProductFields.RelatedAWSResources:0/type`|`ProductFields.RelatedAWSResources:0/type`|
|`unmapped.ProductFields.StandardsControlArn`|`ProductFields.StandardsControlArn`|
|`unmapped.ProductFields.aws/securityhub/ProductName`|`ProductFields.aws/securityhub/ProductName`|
|`unmapped.ProductFields.aws/securityhub/CompanyNam`|`ProductFields.aws/securityhub/CompanyName`|
|`unmapped.ProductFields.Resources:0/Id`|`ProductFields.Resources:0/Id`|
|`unmapped.ProductFields.aws/securityhub/FindingId`|`ProductFields.aws/securityhub/FindingId`|
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
|`unmapped.Compliance_StatusReasons[].Description`|`Compliance.StatusReasons[].Description`|
|`unmapped.Compliance_StatusReasons[].ReasonCode`|`Compliance.StatusReasons[].ReasonCode`|
|`unmapped.Compliance_AssociatedStandards[]`|`Compliance.AssociatedStandards[]`|
|`unmapped.Compliance_SecurityControlId[]`|`Compliance.SecurityControlId[]`|
|`unmapped.FindingProviderFields.Severity.Label`|`FindingProviderFields.Severity.Label`|
|`unmapped.FindingProviderFields.Severity.Original`|`FindingProviderFields.Severity.Original`|
|`unmapped.FindingProviderFields.[]`|`FindingProviderFields.[]`|
|`unmapped.RecordState`|`RecordState`|
|`unmapped.CompanyName`|`CompanyName`|
|`malware[].name`|`Malware[].Name`|
|`malware[].path`|`Malware[].Path`|
|`malware[].classifications[]`|`Malware[].Type`|
|`unmapped.Malware[].Name`|`Malware[].Name`|
|`unmapped.Malware[].Type`|`Malware[].Type`|
|`unmapped.Malware[].Path`|`Malware[].Path`|
|`unmapped.Malware[].State`|`Malware[].State`|
|`unmapped.Vulnerabilities[].Cvss[].BaseScore`|`Vulnerabilities[].Cvss[].BaseScore`|
|`unmapped.Vulnerabilities[].Cvss[].BaseVector`|`Vulnerabilities[].Cvss[].BaseVector`|
|`unmapped.Vulnerabilities[].Cvss[].Version`|`Vulnerabilities[].Cvss[].Version`|
|`unmapped.Vulnerabilities[].Id.`|`Vulnerabilities[].Id`|
|`unmapped.Vulnerabilities[].ReferenceUrls[]`|`Vulnerabilities[].ReferenceUrls[]`|
|`unmapped.Vulnerabilities[].RelatedVulnerabilities`|`Vulnerabilities[].RelatedVulnerabilities`|
|`unmapped.Vulnerabilities[].Vendor.Name`|`Vulnerabilities[].Vendor.Name`|
|`unmapped.Vulnerabilities[].Vendor.Url`|`Vulnerabilities[].Vendor.Url`|
|`unmapped.Vulnerabilities[].Vendor.VendorCreatedAt`|`Vulnerabilities[].Vendor.VendorCreatedAt`|
|`unmapped.Vulnerabilities[].Vendor.VendorSeverity`|`Vulnerabilities[].Vendor.VendorSeverity`|
|`unmapped.Vulnerabilities[].Vendor.VendorUpdatedA`|`Vulnerabilities[].Vendor.VendorUpdatedAt`|
|`unmapped.Vulnerabilities[].VulnerablePackages[].Architecture`|`Vulnerabilities[].VulnerablePackages[].Architecture`|
|`unmapped.Vulnerabilities[].VulnerablePackages[].Epoch`|`Vulnerabilities[].VulnerablePackages[].Epoch`|
|`unmapped.Vulnerabilities[].VulnerablePackages[].Name`|`Vulnerabilities[].VulnerablePackages[].Name`|
|`unmapped.Vulnerabilities[].VulnerablePackages[].Release`|`Vulnerabilities[].VulnerablePackages[].Release`|
|`unmapped.Vulnerabilities[].VulnerablePackages[].Version`|`Vulnerabilities[].VulnerablePackages[].Version`|
