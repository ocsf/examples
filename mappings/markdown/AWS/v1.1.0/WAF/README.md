# Event Dossier: Amazon WAF
### Amazon WAF WebACL logs
- **Description**: Translates Amazon WAF logs to HTTP Activity event class with Security Control Profile in OCSF.
- **Event References**:
  - https://docs.aws.amazon.com/waf/latest/developerguide/logging-fields.html 
  - https://docs.aws.amazon.com/waf/latest/developerguide/logging-examples.html

 ### OCSF Version: 1.1.0
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4002`
 - `class_name`: `HTTP Activity`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud,security_control,datetime]`
 - `metadata.product.name`: `Amazon WAF`
 - `metadata.product.feature.name`: `WAF`
 - `metadata.product.vendor_name`: `AWS`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| Raw                       | OCSF             |
| -------------------------- | ----------------|
|`webaclId`|`metadata.product.feature.uid`|
|`formatVersion`|`metadata.product.version`|
|`labels[]`| `metadata.labels[]`|
|`httpSourceName`|`src_endpoint.svc_name`|
|`httpSourceId`|`src_endpoint.uid`|
|`httpRequest.clientIp`|`src_endpoint.ip`|
|`httpRequest.country`|`src_endpoint.location.country`|
|`httpRequest.uri`|`http_request.url.path`|
|`httpRequest.httpVersion`|`http_request.version`|
|`httpRequest.httpMethod`|`http_request.http_method`|
|`httpRequest.requestId`|`http_request.uid`|
|`httpRequest.args`|`http_request.args`|
|`terminatingRuleId`|`firewall_rule.uid`|
|`terminatingRuleType`|`firewall_rule.type`|
|`terminatingRuleMatchDetails[].conditionType`|`firewall_rule.condition`|
|`terminatingRuleMatchDetails[].location`|`firewall_rule.match_location`|
|`terminatingRuleMatchDetails[].matchedData[]`|`firewall_rule.match_details[]`|
|`rateBasedRuleList[].maxRateAllowed`|`firewall_rule.rate_limit`|
|`responseCodeSent`|`status_code`|


 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| Raw                       | OCSF             | Notes             |
| -------------------------- | ----------------| ------------------|
|`httpRequest.httpMethod`|`activity_name`|
|`httpRequest.httpMethod`|`activity_id`|
|`httpRequest.httpMethod`|`type_uid`|
|`httpRequest.httpMethod`|`type_name`|
|`action`|`action`|
|`action`|`action_id`|
|`action`|`disposition`|
|`action`|`disposition_id`|
|_if `httpRequest.headers[].name` equals `User-Agent`_|
|`httpRequest.headers[].value`|`http_request.user_agent`| 
|_elseif `httpRequest.headers[].name` equals `Host`_|
|`httpRequest.headers[].value`|`http_request.url.hostname`|
|_elseif `httpRequest.headers[].name` equals `X-Forwarded-For`_|
|`httpRequest.headers[].value`|`http_request.x_forwarded_for`|
|_elseif `httpRequest.headers[].name` equals `referer`_|
|`httpRequest.headers[].value`|`http_request.referrer`|
|_else_|
|`httpRequest.headers[].name`|`http_request.http_headers[].name`|
|`httpRequest.headers[].value`|`http_request.http_headers[].value`|


