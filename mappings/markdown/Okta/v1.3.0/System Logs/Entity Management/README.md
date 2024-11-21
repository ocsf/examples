# Event Dossier: Okta system log Entity Management

### An Okta system log for 
- **Description**: Translates a `policy.lifecycle.create` log to OCSF.
- **Event References**:
  - https://developer.okta.com/docs/reference/api/event-types/#catalog

 ### OCSF Version: 1.3.0
  - `class_name`: `Entity Management`
  - `class_uid`: `3004`
  - `category_name`: `Identity & Access Management`
  - `category_uid`: `3`
  - `severity_id`: `1`
  - `severity`: `Informational`
  - `metadata.product.name`: `Okta System Log`
  - `metadata.product.vendor_name`: `Okta`
  - `metadata.profiles`: `[datetime, host]`
  - `metadata.version`: `1.3.0`

### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

Any fields not present in an explicit mapping will be mapped to the unmapped object.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`actor.user.name`|`actor.displayName`|
|`actor.user.email_addr`|`actor.alternateId`|
|`actor.user.uid`|`actor.id`|
|`actor.session.uid`|`authenticationContext.externalSessionId`|
|`actor.session.issuer`|`authenticationContext.issuer.id`|
|`device.uid`|`device.id`|
|`device.name`|`device.name`|
|`entity.policy.name`|`target.displayName`|
|`entity.policy.uid`|`target.id`|
|`message`|`displayMessage`|
|`metadata.event_code`|`eventType`|
|`metadata.product.version`|`version`|
|`metadata.uid`|`uuid`|
|`time`|`published`|
|`http_request.uid`|`debugContext.debugData.requestId`|
|`http_request.url.path`|`debugContext.debugData.url`|
|`http_request.user_agent`|`client.userAgent.rawUserAgent`|
|`src_endpoint.ip`|`client.ipAddress`|
|`src_endpoint.domain`|`securityContext.domain`|
|`src_endpoint.type`|`client.device`|
|`src_endpoint.location.city`|`client.geographicalContext.city`|
|`src_endpoint.location.lat`|`client.geographicalContext.geolocation.lat`|
|`src_endpoint.location.long`|`client.geographicalContext.geolocation.lon`|
|`src_endpoint.location.country`|`client.geographicalContext.country`|
|`src_endpoint.location.isp`|`securityContext.isp`|
|`src_endpoint.location.postal_code`|`client.geographicalContext.postalCode`|
|`src_endpoint.autonomous_system.name`|`securityContext.asOrg`|
|`src_endpoint.autonomous_system.number`|`securityContext.asNumber`|

### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`src_endpoint.os.name/src_endpoint.os.type/src_endpoint.os.type_id`|`client.userAgent.os`|
|`device.type/device.type_id`|`device.os_platform`|
|`status_id/status`|`outcome.result`|
|`entity.type/entity.type_id`|`target.type`|
|`activity_name/activity_id`|`eventType/displayMessage`|


