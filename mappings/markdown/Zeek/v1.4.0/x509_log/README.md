# Event Dossier: Zeek x509.log
### Summary
- **Description**: Translates a Zeek x509.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.4.0/classes/network_activity
  - https://docs.zeek.org/en/master/logs/x509.html
  - https://docs.zeek.org/en/master/scripts/base/files/x509/main.zeek.html#type-X509::Info

 ### OCSF Version: v1.4.0


 ### Static value mapping
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.4.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4001         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |
| `activity_id`                       | 99           | Integer    |
| `activity_name`                     | "Certificate details" |   |
| `type_uid`                          | 300299       | Integer    |
| `service.name`                      | "N/A"        |            |
| `user.name`                         | "N/A"        |            |


 ### Direct field mapping
| OCSF                              | Raw                       | Zeek Field Description                                                                  | Notes                   |
| --------------------------------- | ------------------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                            | `ts`                      | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `start_time`                      | `ts`                      | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `metadata.logged_time`            | `_write_ts`               | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is Integer. |
| `metadata.loggers[].name`         | `_system_name`            | Name of the system or logging subsystem generating the log entry.                       | |
| `tls.certificate.issuer`          | `certificate.issuer`      | Issuer of the certificate.                                                              | |
| `tls.certificate.not_valid_after` | `certificate.expiration_time` | Timestamp after which the certificate is not valid.                                 | Convert to epoch value. <br>Type is Integer. |
| `tls.certificate.not_valid_before`| `certificate.created_time`| Timestamp before which the certificate is not valid.                                    | Convert to epoch value. <br>Type is Integer. |
| `tls.certificate.serial_number`   | `certificate.serial`      | Serial number of the certificate.                                                       | |
| `tls.certificate.subject`         | `certificate.subject`     | Subject of the certificate.                                                             | |
| `tls.certificate.version`         | `certificate.version`     | Version number of the certificate.                                                      | |
| `tls.certificate.sans[]`          | `san.dns{}`               | List of DNS entries in the Subject Alternative Name (SAN) field.                        | |
| `tls.key_length`                  | `certificate.key_length`  | Key length in bits for the certificate.                                                 | |

 ### Conditional mapping
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                                   | Raw                    | Zeek Field Description                                                  | Evaluation Conditions                                                                                                               |
| -------------------------------------- | ---------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `tls.certificate.fingerprints[].value` | `fingerprint`          | Fingerprint of the certificate using the specified signature algorithm. | Where `tls.certificate.fingerprints[].algorithm` = `tls.certificate.sig_alg`                                                        |
| `tls.tls_extension_list.data`          | `basic_constraints.ca` | CA flag set? Indicates if the certificate can sign other certificates.  | Where `tls.tls_extension_list.type_id` = 47 <br>Type is Integer <br>`tls.tls_extension_list.type` will = "certificate_authorities". |
| `tls.tls_extension_list.data`          | `certificate.key_alg`  | Key algorithm used in the certificate.                                  | Where `tls.tls_extension_list.type_id` = 13 <br>Type is Integer <br>`tls.tls_extension_list.type` will = "signature_algorithms".    |

 ### Unmapped (proposed)
| OCSF                                        | Raw                          | Zeek Field Description                                                                 |
| ------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------- |
| `tls.certificate.(curve)`                   | `certificate.curve`          | Curve used in the certificate, if it is an EC-certificate.                             |
| `tls.certificate.(exponent)`                | `certificate.exponent`       | Exponent used in the certificate, if it is an RSA-certificate. <br>Type is Integer.    |
| `tls.certificate.(key_type)`                | `certificate.key_type`       | Key type, such as RSA, DSA, or EC, if parseable by OpenSSL.                            |
| `tls.certificate.(max_cert_chain_path_len)` | `basic_constraints.path_len` | Maximum path length for the certificate chain. <br>Type is Integer.                    |
| `tls.certificate.(is_client_cert)`          | `client_cert`                | Indicates if this certificate was sent from the client. <br>Type is boolean.           |
| `tls.certificate.(is_host_cert)`            | `host_cert`                  | Indicates if this certificate was an end-host certificate, or sent as part of a chain. <br>Type is boolean. |
