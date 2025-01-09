# Event Dossier: Zeek http.log
### Summary:
- **Description**: Translates a Zeek http.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/http_activity
  - https://docs.zeek.org/en/master/logs/http.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/http/main.zeek.html#type-HTTP::Info
    
 ### OCSF Version: v1.3.0


 ### Static value mapping:
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.3.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4002         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |


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
| `dst_endpoint.port`            | `id.resp_p`       | The responder’s port number.                                                            | Type is Integer.        |
| `http_request.http_method`     | `method`          | Verb used in the HTTP request (GET, POST, HEAD, etc.).                                  |                         |
| `http_request.length`          | `request_body_len`| Actual uncompressed content size of the data transferred from the client.               | Type is Integer.        |
| `http_request.referrer`        | `referrer`        | Value of the “referrer” header.                                                         |                         |
| `http_request.url.hostname`    | `dest_host`       |                                                                                         |                         |
| `http_request.url.path`        | `uri`             | URI used in the request.                                                                |                         |
| `http_request.user_agent`      | `user_agent`      | Value of the User-Agent header from the client.                                         |                         |
| `http_request.version`         | `version`         | Value of the version portion of the reply.                                              |                         |
| `http_request.x_forwarded_for` | `proxied`         | All of the headers that may indicate if the request was proxied.                        | Type is IP address.     |
| `http_response.code`           | `status_code`     | Status code returned by the server.                                                     | Type is Integer.        |
| `http_response.length`         | `response_body_len`| Actual uncompressed content size of the data transferred from the server.              | Type is Integer.        |
| `http_response.status`         | `status_msg`      | Status message returned by the server.                                                  |                         |
| `message`                      | `tags`            | A set of indicators of various attributes discovered and related to a particular request/response pair. |         |


### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                              | Raw               | Zeek Field Description                                                                  | Evaluation Conditions                                                                                     |
| --------------------------------- | ----------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `activity_id`          | `method`          | Verb used in the HTTP request (GET, POST, HEAD, etc.). | If "CONNECT", 1, <br>if "DELETE", 2 <br>if "GET", 3 <br>if "HEAD", 4 <br>if "OPTIONS", 5 <br>if "POST", 6 <br>if "PUT", 7 <br>if "TRACE", 8 <br>else 99 where `activity_name` = `method` <br>Type is Integer. |
| `type_uid`             | `method`          | Verb used in the HTTP request (GET, POST, HEAD, etc.). | (`class_uid` * 100) + `activity_id` |
| `http_cookies[].value` | `cookie`          | Cookie value used by the client machine. | Where `http_cookies[].name` = "Request Cookie"  |
| `http_cookies[].value` | `resp_cookie`     |  | Where `http_cookies[].name` = "Response Cookie" |
| `http_request.http_headers[].value` | `accept_language` |  | Where `http_request.http_headers[].name` = "Accept Language"                                                |
| `http_request.http_headers[].value` | `accept_encoding` |  | Where `http_request.http_headers[].name` = "Accept Encoding"                                                |
| `http_request.http_headers[].value` | `accept`          |  | Where `http_request.http_headers[].name` = "Accept"                                                         |
| `http_request.http_headers[].value` | `post_body`       | The post_body information. | Where `http_request.http_headers[].name` = "Body"                                 |
| `http_request.http_headers[].value` | `origin`          | Value of the Origin header from the client. | Where `http_request.http_headers[].name` = "Origin"              |
| `http_request.http_headers[].value` | `client_headers`  |  | Where `http_request.http_headers[].name` = "Client Headers"                                                 |
| `http_response.http_headers[].value`| `server_headers`  |  | Where `http_response.http_headers[].name` = "Server Headers"                                                |


 ### Unmapped (proposed):
| OCSF                              | Raw                      | Zeek Field Description                                                                  |
| ----------------------------------| -------------------------| --------------------------------------------------------------------------------------- |
| `http_request.(file.names[])`     | `orig_filenames`         | An ordered vector of filenames from the client.                                         |
| `http_response.(file.names[])`    | `resp_filenames`         | An ordered vector of filenames from the server.                                         |
| `http_request.(file.mime_types[])`| `orig_mime_types`        | An ordered vector of mime types.                                                        |
| `http_response.(file.mime_types[])`| `resp_mime_types`       | An ordered vector of mime types.                                                        |
| `http_request.(file.uids[])`      | `orig_fuids`             | An ordered vector of file unique IDs.                                                   |
| `http_response.(file.uids[])`     | `resp_fuids`             | An ordered vector of file unique IDs.                                                   |
| `unmapped`                        | `trans_depth`            | Represents the pipelined depth into the connection of this request/response transaction.|
| `unmapped`                        | `if_none_match`          |                                                                                         |
| `unmapped`                        | `if_modified_since`      |                                                                                         |
| `observables[].value`             | `username`               | Username if basic-auth is performed for the request.                                    |