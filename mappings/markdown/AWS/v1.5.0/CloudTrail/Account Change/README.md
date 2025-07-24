# Event Dossier: Amazon CloudTrail Account Change API Activity

### A CloudTrail event for CreateUser API
- **Description**: Translates a CreateUser Event to OCSF.
- **Event References**:
  - https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-examples.html

 ### OCSF Version: 1.5.0
  - `class_name`: `Account Change`
  - `class_uid`: `3001`
  - `category_name`: `Identity & Access Management`
  - `category_uid`: `3`
  - `cloud.provider`: `AWS`
  - `severity_id`: `1`
  - `severity`: `Informational`
  - `metadata.product.name`: `CloudTrail`
  - `metadata.product.vendor_name`: `AWS`
  - `metadata.profiles`: `[cloud, datetime]`
  - `metadata.version`: `1.5.0`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

- Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                            | Raw                                                       |
|:--------------------------------|:----------------------------------------------------------|
| `actor.idp.name`                | `userIdentity.identityProvider`                           |
| `actor.idp.name`                | `userIdentity.webIdFederationData.federatedProvider`      |
| `actor.invoked_by`              | `userIdentity.invokedBy`                                  |
| `actor.session.created_time_dt` | `userIdentity.sessionContext.attributes.creationDate`     |
| `actor.session.is_mfa`          | `userIdentity.sessionContext.attributes.mfaAuthenticated` |
| `actor.session.issuer`          | `userIdentity.sessionContext.sessionIssuer.arn`           |
| `actor.user.account.uid`        | `userIdentity.accountId`                                  |
| `actor.user.credential_uid`     | `userIdentity.accessKeyId`                                |
| `actor.user.name`               | `userIdentity.userName`                                   |
| `actor.user.type`               | `userIdentity.type`                                       |
| `actor.user.uid`                | `userIdentity.arn`                                        |
| `actor.user.uid_alt`            | `userIdentity.principalId`                                |
| `api.operation`                 | `eventName`                                               |
| `api.request.data`              | `requestParameters`                                       |
| `api.response.data`             | `responseElements`                                        |
| `api.response.error`            | `errorCode`                                               |
| `api.response.message`          | `errorMessage`                                            |
| `api.service.name`              | `eventSource`                                             |
| `api.version`                   | `apiVersion`                                              |
| `cloud.account.uid`             | `recipientAccountId`                                      |
| `cloud.region`                  | `awsRegion`                                               |
| `http_request.user_agent`       | `userAgent`                                               |
| `metadata.event_code`           | `eventType`                                               |
| `metadata.product.version`      | `eventVersion`                                            |
| `metadata.uid`                  | `eventID`                                                 |
| `policy.uid`                    | `requestParameters.policyArn`                             |
| `src_endpoint.uid`              | `vpcEndpointId`                                           |
| `time`                          | `eventTime`                                               |
| `time_dt`                       | `eventTime`                                               |

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`metadata.product.feature.name`|`eventCategory`|
|`api.request.uid`|`requestID`|
|`user.uid`|`userIdentity.principalId/responseElements.role.roleId/responseElements.user.userId`|
|`user.name`|`responseElements.role.path/responseElements.role.description/requestParameters.userName/responseElements.role.roleName/responseElements.user.userName/requestParameters.roleName`|
|`src_endpoint.ip/src_endpoint.domain`|`sourceIPAddress`|
|`status`|`errorCode`|
|`activity_name/activity_id/type_uid/type_name`|`eventName`|
|`actor.user.credential_uid`|`userIdentity.credentialId`|
|`actor.user.name`|`additionalEventData.UserName`|
|`actor.user.uid_alt`|`userIdentity.onBehalfOf.userId`|
|`actor.idp.uid`|`userIdentity.onBehalfOf.identityStoreArn`|

### Observables:

- All Hostnames, IP Addresses, User Names, Resource ARNs will be populated as observables in each record. These will conform to the observable types described in [OCSF](https://schema.ocsf.io/1.5.0/objects/observable).
