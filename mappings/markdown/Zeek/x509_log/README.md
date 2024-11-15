# Event Dossier: Zeek x509.log
### Summary:
- **Description**: Translates a Zeek x509.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/authentication
  - https://docs.zeek.org/en/master/logs/x509.html
  - https://docs.zeek.org/en/master/scripts/base/files/x509/main.zeek.html#type-X509::Info
    
 ### Static mapping: OCSF Version 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Identity & Access Management`
 - `category_uid`: `3`
 - `class_name`: `Authentication`
 - `class_uid`: `3002`
 - `metadata.log_name`: `x509.log`
 - `metadata.loggers[].log_provider`: `Zeek`
 - `metadata.loggers[].product.name`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `x509.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/x509.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:

| OCSF                          | Raw             | Notes           |
| ----------------------------- | --------------- | --------------- |
|`time`                         |`ts`             | |
|`start_time`                   |`ts`             | |
|`metadata.logged_time`         |`_write_ts`      | |
|`metadata.loggers[].name`      |`_system_name`   | |
|`certificate.fingerprints[].value` |`fingerprint`   | In a record where `certificate.fingerprints[].algorithm` = `certificate.sig_alg` |
|`certificate.issuer`           |`certificate.issuer`    | |
|`certificate.not_valid_after`  |`certificate.expiration_time`| |
|`certificate.not_valid_before` |`certificate.created_time`   | |
|`certificate.serial_number`    |`certificate.serial`    | |
|`certificate.subject`          |`certificate.subject`   | |
|`certificate.version`          |`certificate.version`   | |
|`observables[].value`          |`san.dns{}`      | In a record where observables[].type_id = "1" AND observables[].type = "Hostname" |

 ### Unmapped:
| OCSF            | Raw                        | Notes           |
| --------------- | -------------------------- | --------------- |
|`unmapped`       |`basic_constraints.ca`      | boolean |
|`unmapped`       |`basic_constraints.path_len`| int |
|`unmapped`       |`certificate.curve`         | |
|`unmapped`       |`certificate.exponent`      | |
|`unmapped`       |`certificate.key_alg`       | |
|`unmapped`       |`certificate.key_length`    | |
|`unmapped`       |`certificate.key_type`      | |
|`unmapped`       |`client_cert`               | boolean |
|`unmapped`       |`host_cert`                 | boolean |
