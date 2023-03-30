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
|`finding.create_time`|`CreatedAt`|
|`finding.modified_time`|`UpdatedAt`|
|`severity`|`Severity.Label`|
|`unmapped.Severity_Original`|`Severity.Original`|
|`unmapped.Severity_Normalized`|`Severity.Normalized`|
|`unmapped.Severity_Product`|`Severity.Product`|
