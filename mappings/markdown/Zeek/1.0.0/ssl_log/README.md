# Event Dossier: Zeek ssl.log
### 
- **Description**: Translates a Zeek ssl.log to OCSF. 
- **Event References**:
  - https://docs.zeek.org/en/master/logs/ssl.html
  - https://schema.ocsf.io/1.0.0-rc.3/classes/network_activity
 
 ### OCSF Version: 1.0.0-rc.3
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4001`
 - `class_name`: `Network Activity`
 - `metadata.profiles`: `[security_control]`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.feature.name`: `ssl.log`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                           | Raw               |
| ------------------------------ | ----------------- |
|'time'                          |'ts'               |
|'uuid'                          |'uid'              |
|'src_endpoint.ip'               |'id.orig_h'        |
|'src_endpoint.port'             |'id.orig_p'        |
|'dst_endpoint.ip'               |'id.resp_h'        |
|'dst_endpoint.port'             |'id.resp_p'        |
|'version'                       |'version'          |
|'cipher'                        |'cipher'           |
|'certificate'                   |'curve'            |
|'domain'                        |'server_name'      |
|'certificate_chain'             |'cert_chain_fluids'|
|'subject'                       |'subject'          |
|'issuer'                        |'issuer'           |
|'unmapped'                      |'next_protocol'    |
|'unmapped'                      |'resumed'          |
|'network_activity.status_id':'1'|'established'      |

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                          | Raw               | Notes              |
| ------------------------------| ------------------| -- ----------------|


 ### Proposed New OCSF attributes:
 - 
| OCSF                     | Raw                      |
| -------------------------| -------------------------|
|'client_certificate_chain'|'client_cert_chain_fluids'|
