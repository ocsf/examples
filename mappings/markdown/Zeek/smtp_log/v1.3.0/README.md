# Event Dossier: Zeek smtp.log
### Summary:
- **Description**: Translates a Zeek smtp.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/email_activity
  - https://docs.zeek.org/en/master/logs/smtp.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/smtp/main.zeek.html#type-SMTP::Info
    
 ### OCSF Version: v1.3.0
 
 ### Static mapping:
| OCSF field                          | Value                                           |
| ----------------------------------- | ----------------------------------------------- |
| `metadata.version`                  | "1.3.0"                                         |
| `category_name`                     | "Network Activity"                              |
| `category_uid`                      | "4"                                             |
| `class_name`                        | "Email Activity"                                |
| `class_uid`                         | "4009"                                          |
| `metadata.log_name`                 | "smtp.log"                                      |
| `metadata.loggers[].log_provider`   | "Zeek"                                          |
| `metadata.loggers[].product.name`   | "Zeek"                                          |
| `metadata.product.cpe_name`         | "cpe:2.3:a:zeek:zeek"                           |
| `metadata.product.feature.name`     | "smtp.log"                                      |
| `metadata.product.name`             | "Zeek"                                          |
| `metadata.product.url_string`       | "https://docs.zeek.org/en/current/logs/smtp.html"|
| `metadata.product.vendor_name`      | "Zeek"                                          |
| `severity`                          | "Informational"                                 |
| `severity_id`                       | "1"                                             |

 ### Mapping:
| OCSF                           | Raw               | Zeek Field Description                                                                  |
| ------------------------------ | ----------------- | --------------------------------------------------------------------------------------- |
| `time`                         | `ts`              | Timestamp indicating when the event occurred.                                           |
| `start_time`                   | `ts`              | Timestamp indicating when the event occurred.                                           |
| `metadata.logged_time`         | `_write_ts`       | Timestamp indicating when the log entry was written to disk.                            |
| `metadata.loggers[].name`      | `_system_name`    | Name of the system or logging subsystem generating the log entry.                       |
| `metadata.uid`                 | `uid`             | Unique ID for the connection.                                                           |
| `src_endpoint.ip`              | `id.orig_h`       | The originator’s IP address.                                                            |
| `src_endpoint.port`            | `id.orig_p`       | The originator’s port number.                                                           |
| `dst_endpoint.ip`              | `id.resp_h`       | The responder’s IP address.                                                             |
| `dst_endpoint.port`            | `id.resp_p`       | The responder’s port number.                                                            |
| `email.message_uid`            | `msg_id`          | Contents of the MsgID header.                                                           |
| `email.from`                   | `from`            | Contents of the From header.                                                            |
| `email.to[]`                   | `to`              | Contents of the To header.                                                              |
| `email.smtp_to[]`              | `rcptto`          | Email addresses found in the Rcpt header.                                               |
| `email.smtp_from`              | `mailfrom`        | Email addresses found in the From header.                                               |
| `smtp_hello`                   | `helo`            | Contents of the Helo header.                                                            |
| `status_detail`                | `last_reply`      | The last message that the server sent to the client.                                    |

 ### Mapping from a different OCSF category:
| OCSF                                      | Raw       | Zeek Field Description                                                                  |
| ----------------------------------------- | --------- | --------------------------------------------------------------------------------------- |
| `email_url_activity.url.hostname`         | `domains` | The domains seen in the email.                                                          |
| `email_url_activity.url.url_string`       | `urls`    | The URLs seen in the email.                                                             |
| `network_activity.proxy.intermediate_ips[]` | `path`  | The message transmission path, as extracted from the headers.                           |
| `network_file_activity.file.uid`          | `fuids`   | An ordered vector of file unique IDs seen attached to the message.                      |

 ### Unmapped (proposed):
| OCSF                     | Raw                | Zeek Field Description                                                                  |
| -------------------------| -------------------| --------------------------------------------------------------------------------------- |
| `unmapped`               | `date`             | Contents of the Date header.                                                            |
| `unmapped`               | `tls`              | Boolean indicator for when the connection has switched to using TLS.                    |
| `(app_name)`             | `is_webmail`       | Boolean indicator of if the message was sent through a webmail interface.               |
