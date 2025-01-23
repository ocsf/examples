# Event Dossier: Zeek x509.log
### Summary:
- **Description**: Translates a Zeek x509.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/authentication
  - https://docs.zeek.org/en/master/logs/x509.html
  - https://docs.zeek.org/en/master/scripts/base/files/x509/main.zeek.html#type-X509::Info
    
 ### OCSF Version: v1.3.0


 ### Static value mapping:
| OCSF field                          | Value       | Type       |
| ----------------------------------- | ----------- | ---------- |
| `metadata.version`                  | "1.3.0"     |            |
| `category_uid`                      | "3"         | Integer    |
| `class_uid`                         | "3002"      | Integer    |
| `severity_id`                       | "1"         | Integer    |
| `metadata.product.name`             | "Zeek"      |            |
| `metadata.product.vendor_name`      | "Zeek"      |            |
| `activity_id`                       | "99"        | Integer    |
| `type_uid`                          | "300299"    | Integer    |
| `service.name`                      | "N/A"       |            |
| `user.name`                         | "N/A"       |            |


 ### Direct field mapping:
| OCSF                          | Raw                       | Zeek Field Description                                                                  | Notes                   |
| ----------------------------- | ------------------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                        | `ts`                      | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `start_time`                  | `ts`                      | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `metadata.logged_time`        | `_write_ts`               | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is Integer. |
| `metadata.loggers[].name`     | `_system_name`            | Name of the system or logging subsystem generating the log entry.                       | |
| `certificate.issuer`          | `certificate.issuer`      | Issuer of the certificate.                                                              | |
| `certificate.not_valid_after` | `certificate.expiration_time` | Timestamp after which the certificate is not valid.                                 | |
| `certificate.not_valid_before`| `certificate.created_time`| Timestamp before which the certificate is not valid.                                    | |
| `certificate.serial_number`   | `certificate.serial`      | Serial number of the certificate.                                                       | |
| `certificate.subject`         | `certificate.subject`     | Subject of the certificate.                                                             | |
| `certificate.version`         | `certificate.version`     | Version number of the certificate.                                                      | |

 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                               | Raw              | Zeek Field Description                                                                 | Evaluation Conditions                                                               |
| ---------------------------------- | ---------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `certificate.fingerprints[].value` | `fingerprint`    | Fingerprint of the certificate using the specified signature algorithm.                | Where `certificate.fingerprints[].algorithm` = `certificate.sig_alg`                |
| `observables[].value`              | `san.dns{}`      | List of DNS entries in the Subject Alternative Name (SAN) field.                       | Where `observables[].type_id` = "1" AND `observables[].type` = "Hostname" AND `observables[].name` = "certificate.subject"  |

 ### Unmapped:
| OCSF            | Raw                        | Zeek Field Description                                                                  |
| --------------- | -------------------------- | --------------------------------------------------------------------------------------- |
| `unmapped`      | `basic_constraints.ca`     | CA flag set? Indicates if the certificate can sign other certificates.                  |
| `unmapped`      | `basic_constraints.path_len`| Maximum path length for the certificate chain.                                         |
| `unmapped`      | `certificate.curve`        | Curve used in the certificate, if it is an EC-certificate.                              |
| `unmapped`      | `certificate.exponent`     | Exponent used in the certificate, if it is an RSA-certificate.                          |
| `unmapped`      | `certificate.key_alg`      | Key algorithm used in the certificate.                                                  |
| `unmapped`      | `certificate.key_length`   | Key length in bits for the certificate.                                                 |
| `unmapped`      | `certificate.key_type`     | Key type, such as RSA, DSA, or EC, if parseable by OpenSSL.                             |
| `unmapped`      | `client_cert`              | Indicates if this certificate was sent from the client.                                 |
| `unmapped`      | `host_cert`                | Indicates if this certificate was an end-host certificate, or sent as part of a chain.  |
