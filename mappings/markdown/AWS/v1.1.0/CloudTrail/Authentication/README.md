# Event Dossier: Amazon CloudTrail Authentication API Activity

### A CloudTrail event for ConsoleLogin API
- **Description**: Translates a ConsoleLogin Event to OCSF.
- **Event References**:
  - https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-examples.html

 ### OCSF Version: 1.1.0
  - `class_name`: `Authentication`
  - `class_uid`: `3002`
  - `category_name`: `Identity & Access Management`
  - `category_uid`: `3`
  - `cloud.provider`: `AWS`
  - `severity_id`: `1`
  - `severity`: `Informational`
  - `metadata.product.name`: `CloudTrail`
  - `metadata.product.vendor_name`: `AWS`
  - `metadata.profiles`: `[cloud, datetime]`
  - `metadata.version`: `1.1.0`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

- Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`actor.user.account.uid`|`userIdentity.accountId`|
|`actor.user.credential_uid`|`userIdentity.accessKeyId`|
|`actor.user.name`|`userIdentity.userName`|
|`actor.user.type`|`userIdentity.type`|
|`actor.user.uid_alt`|`userIdentity.principalId`|
|`actor.user.uid`|`userIdentity.arn`|
|`actor.session.created_time_dt`|`userIdentity.sessionContext.attributes.creationDate`|
|`actor.session.is_mfa`|`userIdentity.sessionContext.attributes.mfaAuthenticated`|
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
|`metadata.event_code`|`eventType`|
|`time`|`eventTime`|
|`time_dt`|`eventTime`|
|`api.response.error`|`errorCode`|
|`api.response.message`|`errorMessage`|
|`api.request.data`|`requestParameters`|
|`api.response.data`|`responseElements`|
|`dst_endpoint.svc_name`|`additionalEventData.LoginTo`|

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.product.feature.name`|`eventCategory`|
|`src_endpoint.domain/src_endpoint.ip`|`sourceIPAddress`|
|`api.request.uid`|`requestID`|
|`user.uid_alt`|`userIdentity.principalId`|
|`user.uid`|`requestParameters.roleArn/userIdentity.arn`|
|`user.name`|`requestParameters.roleSessionName`|
|`status`|`responseElements.ConsoleLogin`|
|`is_mfa`|`additionalEventData.MFAUsed`|
|`activity_name/activity_id/type_name/type_name/type_uid`|`eventName`|

### Observables:

- All Hostnames, IP Addresses, User Names, Resource ARNs will be populated as observables in each record. These will conform to the observable types described in [OCSF](https://schema.ocsf.io/1.1.0/objects/observable).
