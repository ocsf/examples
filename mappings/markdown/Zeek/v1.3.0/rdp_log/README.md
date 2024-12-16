# Event Dossier: Zeek rdp.log
### Summary:
- **Description**: Translates a Zeek rdp.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/rdp_activity
  - https://docs.zeek.org/en/master/logs/rdp.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/rdp/main.zeek.html#type-RDP::Info

 ### OCSF Version: v1.3.0
 

  ### Static value mapping:
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.3.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4005         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |
| `dst_endpoint.agent_list[].name`    | "RDP Server" |            |
| `dst_endpoint.agent_list[].type_id` | 9            | Integer    |
| `src_endpoint.agent_list[].name`    | "RDP Client" |            |
| `src_endpoint.agent_list[].type_id` | 9            | Integer    |
| `activity_id`                       | 6            | Integer    |
| `type_uid`                          | 400506       | Integer    |


 ### Mapping:

| OCSF                           | Raw                    | Zeek Field Description                                                                  | Notes                   |
| ------------------------------ | ---------------------- | --------------------------------------------------------------------------------------- | ----------------------- |
| `time`                         | `ts`                   | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `start_time`                   | `ts`                   | Timestamp indicating when the event occurred.                                           | Convert to epoch value. <br>Type is Integer. |
| `metadata.logged_time`         | `_write_ts`            | Timestamp indicating when the log entry was written to disk.                            | Convert to epoch value. <br>Type is Integer. |
| `metadata.loggers[].name`      | `_system_name`         | Name of the system or logging subsystem generating the log entry.                       |                         |
| `metadata.log_name`            | `_path`                | Log name.                                                                               |                         |
| `metadata.uid`                 | `uid`                  | Unique ID for the connection.                                                           |                         |
| `src_endpoint.ip`              | `id.orig_h`            | The originator’s IP address.                                                            |                         |
| `src_endpoint.port`            | `id.orig_p`            | The originator’s port number.                                                           | Type is Integer.        |
| `src_endpoint.hostname`        | `client_name`          | Name of the client machine.                                                             |                         |
| `src_endpoint.agent_list[].name` | `client_build`       | RDP client version used by the client machine.                                          |                         |
| `src_endpoint.agent_list[].version` | `client_dig_product_id` | Product ID of the client machine.                                                 |                         |
| `dst_endpoint.ip`              | `id.resp_h`            | The responder’s IP address.                                                             |                         |
| `dst_endpoint.port`            | `id.resp_p`            | The responder’s port number.                                                            | Type is Integer.        |
| `identifier_cookie`            | `cookie`               | Cookie value used by the client machine.                                                |                         |
| `status_detail`                | `result`               | Status result for the connection.                                                       |                         |
| `protocol_ver`                 | `security_protocol`    | Security protocol chosen by the server.                                                 |                         |
| `tls.version`                  | `security_protocol`    | Security protocol chosen by the server.                                                 |                         |
| `tls.key_length`               | `encryption_method`    | Encryption method of the connection.                                                    | Type is Integer.        |
| `remote_display.color_depth`   | `requested_color_depth`| The color depth requested by the client in the high_color_depth field.                  | Type is Integer.        |
| `remote_display.physical_height` | `desktop_height`     | Desktop height of the client machine.                                                   |                         |
| `remote_display.physical_width` | `desktop_width`       | Desktop width of the client machine.                                                    |                         |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                           | Raw               | Zeek Field Description                                              | Evaluation Conditions                                                                               |
| ------------------------------ | ----------------- | ------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `status_id`                    | `auth_success`    | Authentication result.                                              | If "true" then "1", <br>if "false" then "2", <br>else "0". <br>Type is Integer.                    |


 ### Unmapped:
| OCSF                     | Raw                | Zeek Field Description                                                                  |
| -------------------------| -------------------| --------------------------------------------------------------------------------------- |
| `unmapped`               | `cert_count`       | The number of certs seen.                                                               |
| `unmapped`               | `cert_permanent`   | Indicates if the provided certificate or certificate chain is permanent or temporary.   |
| `unmapped`               | `cert_type`        | If the connection is being encrypted with native RDP encryption, this is the type of cert being used. |
| `unmapped`               | `channels_joined`  | The number of channels a client joined during the connection sequence.                  |
| `unmapped`               | `client_channels`  | The channels requested by the client.                                                   |
| `unmapped`               | `encryption_level` | Encryption level of the connection.                                                     |
| `observables[].value`          | `rdfp_hash`       | The rdfp_hash information.                                                              | In an object where `observables[].type_id` = "30", <br>and `observables[].name` = "rdfp_hash".       |
| `observables[].value`          | `rdfp_string`     | A fingerprint which represents an RDP client.                                           | In an object where `observables[].type_id` = "99", <br>and `observables[].type` = "RDP client fingerprint" <br>and `observables[].name` = "rdfp_string".          |
| `observables[].value`          | `keyboard_layout` | Keyboard layout (language) of the client machine.                                       | In an object where `observables[].type_id` = "99", <br>and `observables[].type` = "Client machine keyboard layout language",  <br>and `observables[].name` = "keyboard_layout".          |