# Event Dossier: Okta system log Detection Finding

### An Okta system log for 
- **Description**: Translates a `security.threat.detected` log to OCSF.
- **Event References**:
  - https://developer.okta.com/docs/reference/api/event-types/#catalog

 ### OCSF Version: 1.3.0
  - `class_name`: `Detection Finding`
  - `class_uid`: `2004`
  - `category_name`: `Finding`
  - `category_uid`: `2`
  - `severity_id`: `1`
  - `severity`: `Informational`
  - `metadata.product.name`: `Okta System Log`
  - `metadata.product.vendor_name`: `Okta`
  - `metadata.profiles`: `[datetime, host, security_control]`
  - `metadata.version`: `1.3.0`

### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

Any fields not present in an explicit mapping will be mapped to the unmapped object.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`evidences.src_endpoint.ip`|`client.ipAddress`|
|`evidences.src_endpoint.domain`|`securityContext.domain`|
|`evidences.src_endpoint.type`|`client.device`|
|`evidences.src_endpoint.location.city`|`client.geographicalContext.city`|
|`evidences.src_endpoint.location.lat`|`client.geographicalContext.geolocation.lat`|
|`evidences.src_endpoint.location.long`|`client.geographicalContext.geolocation.lon`|
|`evidences.src_endpoint.location.country`|`client.geographicalContext.country`|
|`evidences.src_endpoint.location.isp`|`securityContext.isp`|
|`evidences.src_endpoint.location.postal_code`|`client.geographicalContext.postalCode`|
|`evidences.src_endpoint.autonomous_system.name`|`securityContext.asOrg`|
|`evidences.src_endpoint.autonomous_system.number`|`securityContext.asNumber`|
|`finding_info.title`|`outcome.reason`|
|`message`|`displayMessage`|
|`metadata.event_code`|`eventType`|
|`metadata.product.version`|`version`|
|`metadata.uid/finding_info.uid`|`uuid`|
|`resources.name`|`debugContext.debugData.url`|
|`time`|`published`|

### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`evidences.src_endpoint.os.name/evidences.src_endpoint.os.type/evidences.src_endpoint.os.type_id`|`client.userAgent.os`|
|`action/action_id/disposition/disposition_id`|`outcome.result`|
