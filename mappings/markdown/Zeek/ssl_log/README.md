# Event Dossier: Zeek ssl.log
### 
- **Description**: Translates a Zeek ssl.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/ssl.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssl/main.zeek.html#type-SSL::Info
    
 ### OCSF Version: 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `Network Activity`
 - `class_uid`: `4001`
 - `metadata.log_name`: `ssl.log`
 - `metadata.loggers.log_provider`: `Zeek`
 - `metadata.loggers.product.name=`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `ssl.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/ssl.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any fields not present in an explicit mapping will be mapped to the unmapped object. 

| OCSF                           | Raw               |
| ------------------------------ | ----------------- |
|'time'                          |'ts'               |
|'start_time'                    |'ts'               |
|'metadata.loggers.logged_time'  |'_write_ts'        |
|'metadata.loggers.name'         |'_system_name'     |
|'metadata.uid'                  |'uid'              |
|'src_endpoint.ip'               |'id.orig_h'        |
|'src_endpoint.port'             |'id.orig_p'        |
|'dst_endpoint.ip'               |'id.resp_h'        |
|'dst_endpoint.port'             |'id.resp_p'        |
|'network_activity.status_id':'1'|'established'      |
|'tls.alert'        |'last_alert' && 'sni_matches_cert'           |
|'tls.cipher'                    |'cipher' && 'curve'|
|'tls.certificate.is_self_signed'             |'validation_status'|
|'tls.certificate.subject'       |'subject'          |
|'tls.certificate.issuer'        |'issuer'           |
|'tls.ja3_hash'                  |'ja3'              |
|'tls.ja3s_hash'                 |'ja3s'             |
|'tls.sni'                       |'server_name'      |
|'tls.version'                       |'version'          |

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                          | Raw               | Notes              |
| ------------------------------| ------------------| -- ----------------|


 ### Proposed New OCSF attributes:
 - 
| OCSF                     | Raw                      |
| -------------------------| -------------------------|
|'network_connection_info.session.(history)' |'established ' && 'resumed' && 'ssl_history' |
|'tls.certificate.fingerprints.value (client)'             |'client_cert_chain_fps'|
|'tls.certificate.fingerprints.value (server)'             |'cert_chain_fps'|
|'unmapped'                      |'next_protocol'    |
