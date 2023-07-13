# Event Dossier: Zeek dns.log
### NOERROR Query Results
- **Description**: Translates a Zeek query log to OCSF. 
- **Event References**:
  - https://docs.zeek.org/en/master/logs/dns.html
  - [https://schema.ocsf.io/1.0.0-rc.3/objects/dns_query](https://schema.ocsf.io/1.0.0-rc.3/classes/dns_activity)

 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4003`
 - `class_name`: `DNS Activity`
 - `metadata.profiles`: `[security_control]`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.feature.name`: `dns.log`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any field not present in an explicit mapping will be moved to the unmapped object.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|''time''|'ts'|
|''uuid''|'uid'|
|''src_endpoint.ip''|'id.orig_h'|
|''src_endpoint.port''|'id.orig_p'|
|''query.hostname''|'query'|
|''query.type''|'qtype_name'|
|''query.class''|'qclass_name'|
|''rcode''|'rcode_name'|
|''rcode_id''|'rcode_name|
|''anwers''|'answers'|
|''dst_endpoint.ip''|'id.resp_h'|
|''dst_endpoint.port''|'id.resp_p'|
|''connection_info.protocol_name''|'proto'|
|''transaction_uid''|'trans_id'|
|''ttl''|'TTLs|




 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|'trans_id'|unmapped'|
|'rtt'|unmapped'|
|'AA'|unmapped'|
|'TC'|unmapped'|
|'RD'|unmapped'|
|'RA'|unmapped'|
|'Z'|unmapped'|
