# Event Dossier: Zeek ftp.log
### Summary:
- **Description**: Translates a Zeek ftp.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/ftp_activity
  - https://docs.zeek.org/en/master/logs/ftp.html
  - https://docs.zeek.org/en/current/scripts/base/protocols/ftp/main.zeek.html
    
 ### OCSF Version: v1.3.0


 ### Static value mapping:
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.3.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4008         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |
| `dst_endpoint.agent_list[].name`    | "FTP Server" |            |
| `dst_endpoint.agent_list[].type_id` | 9            | Integer    |
| `src_endpoint.agent_list[].name`    | "FTP Client" |            |
| `src_endpoint.agent_list[].type_id` | 9            | Integer    |


 ### Direct field mapping:
| OCSF                          | Raw                 | Zeek Field Description                                                                  | Notes                   |
| ----------------------------- | ------------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                        | `ts`                | Time when the connection began.                                                         | Convert to epoch value. <br>Type is Integer. |
| `start_time`                  | `ts`                | Time when the connection began.                                                         | Convert to epoch value. <br>Type is Integer. |
| `metadata.logged_time`        | `_write_ts`         | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is Integer. |
| `metadata.loggers[].name`     | `_system_name`      | Name of the system or logging subsystem generating the log entry.                       |                         |
| `metadata.log_name`           | `_path`             | Log name.                                                                               |                         |
| `metadata.uid`                | `uid`               | Unique ID for the connection.                                                           |                         |
| `src_endpoint.ip`             | `id.orig_h`         | The originator’s IP address.                                                            |                         |
| `src_endpoint.port`           | `id.orig_p`         | The originator’s port number.                                                           | Type is Integer.        |
| `dst_endpoint.ip`             | `id.resp_h`         | The responder’s IP address.                                                             |                         |
| `dst_endpoint.port`           | `id.resp_p`         | The responder’s port number.                                                            | Type is Integer.        |
| `file.size`                   | `file_size`         | Size of the file if the command indicates a file transfer.                              | Type is Integer.        |
| `codes[]`                     | `reply_code`        | Reply code from the server in response to the command.                                  | Type is Integer Array.  |
| `status_code`                 | `reply_code`        | Reply code from the server in response to the command.                                  | Type is String.         |
| `status_detail`               | `reply_msg`         | Reply message from the server in response to the command.                               |                         |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF            | Raw                | Zeek Field Description                                              | Evaluation Conditions                                                             |
| --------------- | -------------------| --------------------------------------------------------------------| ---------------------------------------------------------------------------------------|
| `activity_id`   | `command`          | Command given by the client. | If "STOR" or "APPE" then "1" (Put) <br>if "RETR" then "2" (Get) <br>if "DELE" or "RMD" then "4" (Delete) <br>if "RNFR" or "RNTO" then "5" (Rename) <br>If "LIST" or "NLST" then "6" (List) <br>else "0" (Unknown). |
| `type_uid`      | `class_uid` <br>`activity_id` | | (`class_uid` * 100) + `activity_id`|
| `command`       | `command` && `arg` | Command given by the client, with an optional argument if provided. | If `arg` exists, concatenate `command` and `arg`. |
| `file.name`     | `arg`              | Optional command argument given by the client if provided. | File name may be at the end of the path on the tail end of the `arg` field. |
| `file.type_id`  | `arg`              | Optional command argument given by the client if provided. | File type may inferred by the path in the `arg` field. Map type_id to "1" for Regular File, <br>"2" for Folder, <br>"3" for Character Device, <br>"4" for Block Device, <br>"5" for Local Socket, <br>"6" for Named Pipe, <br>"7" for Symbolic Link, or <br>"0" if the type is unknown. |


 ### Unmapped (proposed):
| OCSF                           | Raw                                            | Zeek Field Description                                              |
| ------------------------------ | -----------------------------------------------| --------------------------------------------------------------------|
| `unmapped`                     | `data_channel.passive`                         | Whether PASV mode is toggled for control channel.  |
| `connection_info.direction_id` | `data_channel.orig_h` && `data_channel.resp_h` | The host that will be initiating the data connection and the host that will be accepting the data connection. | Compare to determine Internal/External/Outbound/Inbound context. |
| `(observables[]).value`        | `user`                                         | User name for the current FTP session.  | Where `observables[].type_id` = "4" |
| `(observables[]).value`        | `password`                                     | Password for the current FTP session if captured. | Where `observables[].type_id` = "99" and  |
