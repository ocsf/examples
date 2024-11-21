# Event Dossier: Zeek ftp.log
### Summary:
- **Description**: Translates a Zeek ftp.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/ftp_activity
  - https://docs.zeek.org/en/master/logs/ftp.html
  - https://docs.zeek.org/en/current/scripts/base/protocols/ftp/main.zeek.html
    
 ### Static mapping: OCSF Version 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `FTP Activity`
 - `class_uid`: `4008`
 - `metadata.log_name`: `ftp.log`
 - `metadata.loggers[].log_provider`: `Zeek`
 - `metadata.loggers[].product.name`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `ftp.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/ftp.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:

| OCSF                          | Raw                 | Zeek Field Description                                                                 |
| ----------------------------- | ------------------- | --------------------------------------------------------------------------------------- |
| `time`                        | `ts`                | Time when the connection began.                                                     |
| `start_time`                  | `ts`                | Time when the connection began.                                                     |
| `metadata.logged_time`        | `_write_ts`         | Timestamp indicating when the log entry was written to disk.                            |
| `metadata.loggers[].name`     | `_system_name`      | Name of the system or logging subsystem generating the log entry.                        |
| `metadata.uid`                | `uid`               | Unique ID for the connection.                                                           |
| `src_endpoint.ip`             | `id.orig_h`         | The originator’s IP address.                                                            |
| `src_endpoint.port`           | `id.orig_p`         | The originator’s port number.                                                           |
| `dst_endpoint.ip`             | `id.resp_h`         | The responder’s IP address.                                                             |
| `dst_endpoint.port`           | `id.resp_p`         | The responder’s port number.                                                            |
| `activity_id`                 | `data_channel.passive` | Whether PASV mode is toggled for control channel.                                     |
| `file.size`                   | `file_size`         | Size of the file if the command indicates a file transfer.                               |
| `ftp_activity.codes`          | `reply_code`        | Reply code from the server in response to the command.                                   |
| `status_code`                 | `reply_code`        | Reply code from the server in response to the command.                                   |
| `status_detailed`             | `reply_msg`         | Reply message from the server in response to the command.                                |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                          | Raw                                 | Evaluation Conditions                                                             | Zeek Field Description                                                                 |
| ----------------------------- | ----------------------------------- | ----------------------------------------------------------------------------------| ---------------------------------------------------------------------------------------|
| `ftp_activity.command`        | `command` && `arg`                  | If `arg` exists, concatenate `command` and `arg`.                                 | Command given by the client, with an optional argument if provided.                    |
| `connection_info.direction`   | `data_channel.orig_h` && `data_channel.resp_h` | Compare to determine Internal/External/Outbound/Inbound context.       | The host that will be initiating the data connection and the host that will be accepting the data connection. |
| `observables[].value`         | `user`                              | Where `observables[].type_id` = `4`                                               | User name for the current FTP session.                                                 |
| `observables[].value`         | `password`                          | Where `observables[].type_id` = `99`                                              | Password for the current FTP session if captured.                                      |
