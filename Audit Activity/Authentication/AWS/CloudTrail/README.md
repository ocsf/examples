# Event Dossier: Amazon CloudTrail Authentication API Activity

### A CloudTrail event for ConsoleLogin API
- **Description**: Translates a ConsoleLogin Event to OCSF.
- **Event References**:
  - https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-examples.html

 ### OCSF Version: 1.0.0-rc.2
  - `class_name`: `Authentication`
  - `class_uid`: `3002`
  - `category_name`: `Audit Activity`
  - `category_uid`: `3`
  - `cloud.provider`: `AWS`
  - `severity_id`: `1`
  - `severity`: `Informational`
  - `metadata.product.name`: `CloudTrail`
  - `metadata.product.vendor_name`: `AWS`
  - `metadata.profiles`: `[cloud]`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`actor.user.account_uid`|`userIdentity.accountId`|
|`actor.user.credential_uid`|`userIdentity.accessKeyId`|
|`actor.user.name`|`userIdentity.userName`|
|`actor.user.type`|`userIdentity.type`|
|`actor.user.uid`|`userIdentity.principalId`|
|`actor.user.uuid`|`userIdentity.arn`|
|`actor.session.created_time`|`userIdentity.sessionContext.attributes.creationDate`|
|`actor.session.mfa`|`userIdentity.sessionContext.attributes.mfaAuthenticated`|
|`actor.session.issuer`|`userIdentity.sessionContext.sessionIssuer.arn`|
|`actor.invoked_by`|`userIdentity.invokedBy`|
|`actor.idp.name`|`userIdentity.webIdFederationData.federatedProvider`|
|`actor.idp.name`|`userIdentity.identityProvider`|
|`src_endpoint.uid`|`vpcEndpointId`|
|`api.service.name`|`eventSource`|
|`api.version`|`apiVersion`|
|`api.operation`|`eventName`|
|`cloud.region`|`awsRegion`|
|`http_request.user_agent`|`userAgent`|
|`metadata.product.version`|`eventVersion`|
|`metadata.uid`|`eventID`|
|`time`|`eventTime`|
|`api.response.error`|`errorCode`|
|`api.response.message`|`errorMessage`|
|`dst_endpoint.svc_name`|`additionalEventData.LoginTo`|

 ### Conditional Mapping:
Any fields described within the conditional mappings are are subject to dynamic mappings contingent on matching a condition within the mapping schema. Fields which fail to meet a particuclar conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.product.feature.name`|`eventCategory`|
|`src_endpoint.domain/src_endpoint.ip`|`sourceIPAddress`|
|`user.uid`|`userIdentity.principalId`|
|`user.uuid`|`requestParameters.roleArn/userIdentity.arn`|
|`user.name`|`requestParameters.roleSessionName`|
|`status/status_id`|`responseElements.ConsoleLogin`|
|`mfa`|`additionalEventData.MFAUsed`|
|`activity_name/activity_id/type_name/type_name/type_uid`|`eventName`|
