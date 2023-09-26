# Event Dossier: Amazon WAF
### Amazon WAF Connection Refused
- **Description**: Translates Amazon WAF event where a connection was refused to OCSF. The source might be in csv or parquet. The source field names may vary with a `-` compared to a `_` depending on the source type. This file has been anonymized and contains only 1 record showing version 5 fields in alphabetical order.
- **Event References**:
  - https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html

 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4002`
 - `class_name`: `HTTP Activity`
 - `cloud.provider`: `AWS`
 - `metadata.profiles`: `[cloud, firewall]`
 - `metadata.product.name`: `Amazon WAF`
 - `metadata.product.feature.name`: `WAF`
 - `metadata.product.vendor_name`: `AWS`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|`webaclId`|`metadata.product.feature.uid`|
|`formatVersion`|`metadata.product.version`|
|`labels[]`| `metadata.labels[]`|
|`httpSourceName`|`src_endpoint.svc_name`|
|`httpSourceId`|`src_endpoint.uid`|
|`httpRequest.clientIp`|`src_endpoint.ip`|
|`httpRequest.country`|`src_endpoint.location.country`|
|`httpRequest.uri`|`http_request.url.path`|
|`httpRequest.uri`|`dst_endpoint.domain`|
|`httpRequest.httpVersion`|`http_request.version`|
|`httpRequest.httpMethod`|`http_request.http_method`|
|`httpRequest.requestId`|`http_request.uid`|
|`terminatingRuleId`|`firewall_rule.uid`|
|`terminatingRuleType`|`firewall_rule.type`|
|`httpRequest.args`|`http_request.args`|
|`terminatingRuleMatchDetails[].conditionType`|`firewall_rule.condition`|
|`terminatingRuleMatchDetails[].location`|`firewall_rule.match_location`|
|`terminatingRuleMatchDetails[].matchedData[]`|`firewall_rule.match_details[]`|
|`rateBasedRuleList[].maxRateAllowed`|`firewall_rule.rate_limit`|
|`requestHeadersInserted[].name`|`http_request.http_headers[].name`|
|`requestHeadersInserted[].value`|`http_request.http_headers[].value`|
|`responseCodeSent`|`firewall_rule.status_code`|




 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             | Notes             |
| -------------------------- | ----------------| ------------------|
|`activity_name`|`httpRequest.httpMethod`|
|`activity_id`|`httpRequest.httpMethod`|
|`type_uid`|`httpRequest.httpMethod`|
|`type_name`|`httpRequest.httpMethod`|
|`action`|`http_response.code`|
|`disposition`|`action`|
|`disposition_id`|`action`|
|`ttpRequest.headers[].name.referer`|`http_request.referrer`|
|`httpRequest.headers[].name.X-Forwarded-Port`|`http_request.url.port`|
|`httpRequest.headers[].name`|`http_request.http_headers[].name`|
|_if `httpRequest.headers[].name` equals `User-Agent`_ - |
|`httpRequest.headers[].name.value`|`http_request.user_agent`|
|_elseif `httpRequest.headers[].name` equals `Host`_ - |
|_concat_|
|`httpRequest.headers[].value;httpRequest.uri;httpRequest.args`|`http_request.url.hostname`|
|_elseif `httpRequest.headers[].name` equals `X-Forwarded-Fort`_ - |
|`httpRequest.headers[].name.value`|`http_request.x_forwarded_for`|
|_elseif `httpRequest.headers[].name` equals `referer`_ - |
|`httpRequest.headers[].name.value`|`http_request.referrer`|
|_elseif `httpRequest.headers[].name` equals `X-Forwarded-Port`_ - |
|`httpRequest.headers[].name.value`|`http_request.url.port`|
|_else_|
|`httpRequest.headers[].name.value`|`http_request.http_headers[].name`|


