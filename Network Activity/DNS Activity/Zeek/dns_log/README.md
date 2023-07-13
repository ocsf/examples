# Event Dossier: Zeek Query Log
### NOERROR Query Results
- **Description**: Translates a Zeek query log to OCSF. 
- **Event References**:
  - https://docs.zeek.org/en/master/logs/dns.html
  - https://schema.ocsf.io/1.0.0-rc.3/objects/dns_query

 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4003`
 - `class_name`: `DNS Activity`
 - `metadata.profiles`: `[security_control]`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.feature.name`: `Query Logs`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any field not present in an explicit mapping will be moved to the unmapped object.

| OCSF                       | Raw             |
| -------------------------- | ----------------|
|'time'|'time'|
|'packet_uid'|'packet_uid'|
|'src_endpoint.ip'|'src_endpoint.ip'|
|'srce_endpoint.port'|'srce_endpoint.port'|
|'id.resp_h'|'id.resp_h'|
|'id.resp_p'|'id.resp_p'|
|'connection_info.protocol_name'|'connection_info.protocol_name'|
|'transaction_uid'|'transaction_uid'|
|'query.hostname'|'query.hostname'|
|'query.class'|'query.class'|
|'opcode'|'opcode'|
|'rcode'|'rcode'|
|'rcode_id'|'rcode_id'|
|answers'|'answers'|
|'type'|'type'|



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
|'TTLs'|unmapped'|
