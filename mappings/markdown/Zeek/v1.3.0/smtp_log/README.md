# Event Dossier: Zeek smtp.log
### Summary:
- **Description**: Translates a Zeek smtp.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/email_activity
  - https://docs.zeek.org/en/master/logs/smtp.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/smtp/main.zeek.html#type-SMTP::Info
    
 ### OCSF Version: v1.3.0
 

 ### Static value mapping:
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.3.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4009         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |
| `direction_id`                      | 0            | Integer    |
| `type_uid`                          | 400903       | Integer    |


 ### Direct field mapping:
| OCSF                           | Raw               | Zeek Field Description                                                                  | Notes                   |
| ------------------------------ | ----------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                         | `ts`              | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `start_time`                   | `ts`              | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `metadata.logged_time`         | `_write_ts`       | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is Integer. |
| `metadata.loggers[].name`      | `_system_name`    | Name of the system or logging subsystem generating the log entry.                       |                         |
| `metadata.log_name`            | `_path`           | Log name.                                                                               |                         |
| `metadata.uid`                 | `uid`             | Unique ID for the connection.                                                           |                         |
| `src_endpoint.ip`              | `id.orig_h`       | The originator’s IP address.                                                            |                         |
| `src_endpoint.port`            | `id.orig_p`       | The originator’s port number.                                                           | Type is Integer.        |
| `dst_endpoint.ip`              | `id.resp_h`       | The responder’s IP address.                                                             |                         |
| `dst_endpoint.port`            | `id.resp_p`       | The responder’s port number.                                                            |                         |
| `email.message_uid`            | `msg_id`          | Contents of the MsgID header.                                                           | Type is Integer.        |
| `email.from`                   | `from`            | Contents of the From header.                                                            | Type is email address.  |
| `email.to[]`                   | `to`              | Contents of the To header.                                                              | OCSF v1.3.0 may incorrectly type this as only the email address. |
| `email.smtp_to[]`              | `rcptto`          | Email addresses found in the Rcpt header.                                               | Type is email address.  |
| `email.smtp_from`              | `mailfrom`        | Email addresses found in the From header.                                               | Type is email address.  |
| `smtp_hello`                   | `helo`            | Contents of the Helo header.                                                            |                         |
| `status_detail`                | `last_reply`      | The last message that the server sent to the client.                                    |                         |


 ### Unmapped (proposed):
| OCSF                     | Raw                | Zeek Field Description                                                                  |
| -------------------------| -------------------| --------------------------------------------------------------------------------------- |
| `unmapped`               | `date`             | Contents of the Date header.                                                            |
| `unmapped`               | `tls`              | Boolean indicator for when the connection has switched to using TLS.                    |
| `(app_name)`             | `is_webmail`       | Boolean indicator of if the message was sent through a webmail interface.               |
| `(email_url_activity).url.hostname`         | `domains` | The domains seen in the email.                                                          |
| `(email_url_activity).url.url_string`       | `urls`    | The URLs seen in the email.                                                             |
| `(network_activity).proxy.intermediate_ips[]` | `path`  | The message transmission path, as extracted from the headers.                           |
| `(network_file_activity).file.uid`          | `fuids`   | An ordered vector of file unique IDs seen attached to the message.                      |