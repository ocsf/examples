# Event Dossier: Zeek ssl.log
### Summary:
- **Description**: Translates a Zeek ssl.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/ssl.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/ssl/main.zeek.html#type-SSL::Info


 ### Static mapping: OCSF Version 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `Network Activity`
 - `class_uid`: `4001`
 - `metadata.log_name`: `ssl.log`
 - `metadata.loggers[].log_provider`: `Zeek`
 - `metadata.loggers[].product.name`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `ssl.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/ssl.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`


 ### Field Mapping:

| OCSF                           | Raw               |
| ------------------------------ | ----------------- |
|`time`                          |`ts`               |
|`start_time`                    |`ts`               |
|`metadata.loggers[].logged_time`|`_write_ts`        |
|`metadata.loggers[].name`       |`_system_name`     |
|`metadata.uid`                  |`uid`              |
|`src_endpoint.ip`               |`id.orig_h`        |
|`src_endpoint.port`             |`id.orig_p`        |
|`dst_endpoint.ip`               |`id.resp_h`        |
|`dst_endpoint.port`             |`id.resp_p`        |
|`network_activity.status_id`:`1`|`established`      |
|`tls.alert`                     |`last_alert`       |
|`tls.cipher`                    |`cipher`           |
|`tls.certificate.is_self_signed`|`validation_status`|
|`tls.certificate.subject`       |`subject`          |
|`tls.certificate.issuer`        |`issuer`           |
|`tls.ja3_hash`                  |`ja3`              |
|`tls.ja3s_hash`                 |`ja3s`             |
|`tls.sni`                       |`server_name`      |
|`tls.version`                   |`version`          |


 ### Unmapped (proposed):

| OCSF                     | Raw                      |
| -------------------------| -------------------------|
|`network_connection_info.session.(history)` |`established ` && `resumed` && `ssl_history` |
|`tls.certificate.fingerprints.value (client)`       |`client_cert_chain_fps`|
|`tls.certificate.fingerprints.value (server)`       |`cert_chain_fps`|
|`unmapped`                      |`curve`            |
|`unmapped`                      |`next_protocol`    |
|`unmapped`                      |`sni_matches_cert` |
