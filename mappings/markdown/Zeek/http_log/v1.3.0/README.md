# Event Dossier: Zeek http.log
### Summary:
- **Description**: Translates a Zeek http.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/http_activity
  - https://docs.zeek.org/en/master/logs/http.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/http/main.zeek.html#type-HTTP::Info
    
 ### OCSF Version: v1.3.0

 ### Static mapping
| OCSF field                          | Value                                           |
| ----------------------------------- | ----------------------------------------------- |
| `metadata.version`                  | "1.3.0"                                         |
| `category_name`                     | "Network Activity"                              |
| `category_uid`                      | "4"                                             |
| `class_name`                        | "HTTP Activity"                                 |
| `class_uid`                         | "4002"                                          |
| `metadata.log_name`                 | "http.log"                                      |
| `metadata.loggers[].log_provider`   | "Zeek"                                          |
| `metadata.loggers[].product.name`   | "Zeek"                                          |
| `metadata.product.cpe_name`         | "cpe:2.3:a:zeek:zeek"                           |
| `metadata.product.feature.name`     | "http.log"                                      |
| `metadata.product.name`             | "Zeek"                                          |
| `metadata.product.url_string`       | "https://docs.zeek.org/en/current/logs/http.html"|
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
| `http_request.http_method`     | `method`          | Verb used in the HTTP request (GET, POST, HEAD, etc.).                                  |
| `http_request.length`          | `request_body_len`| Actual uncompressed content size of the data transferred from the client.               |
| `http_request.referrer`        | `referrer`        | Value of the “referrer” header.                                                         |
| `http_request.url.hostname`    | `dest_host`       | (No description available)                                                              |
| `http_request.url.path`        | `uri`             | URI used in the request.                                                                |
| `http_request.user_agent`      | `user_agent`      | Value of the User-Agent header from the client.                                         |
| `http_request.version`         | `version`         | Value of the version portion of the reply.                                              |
| `http_request.x_forwarded_for` | `proxied`         | All of the headers that may indicate if the request was proxied.                        |
| `http_response.code`           | `status_code`     | Status code returned by the server.                                                     |
| `http_response.length`         | `response_body_len`| Actual uncompressed content size of the data transferred from the server.              |
| `http_response.status`         | `status_msg`      | Status message returned by the server.                                                  |
| `message`                      | `tags`            | A set of indicators of various attributes discovered and related to a particular request/response pair. |

 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                              | Raw               | Evaluation Conditions                                                                                     | Zeek Field Description                                                                  |
| --------------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `http_request.http_cookies[].value` | `cookie`        | Where `http_request.http_cookies[].name` = "Request Cookie"                                               | Cookie value used by the client machine.                                                |
| `http_request.http_headers[].value` | `accept_language` | Where `http_request.http_headers[].name` = "Accept Language"                                                |                                                               |
| `http_request.http_headers[].value` | `accept_encoding` | Where `http_request.http_headers[].name` = "Accept Encoding"                                                |                                                               |
| `http_request.http_headers[].value` | `accept`          | Where `http_request.http_headers[].name` = "Accept"                                                         |                                                               |
| `http_request.http_headers[].value` | `post_body`       | Where `http_request.http_headers[].name` = "Body"                                                           | The post_body information.                                                              |
| `http_request.http_headers[].value` | `origin`          | Where `http_request.http_headers[].name` = "Origin"                                                         | Value of the Origin header from the client.                                             |
| `http_request.http_headers[].value` | `client_headers`  | Where `http_request.http_headers[].name` = "Client Headers"                                                 |                                                               |
| `http_response.http_cookies[].value`| `resp_cookie`     | Where `http_response.http_cookies[].name` = "Response Cookie"                                               |                                                               |
| `http_response.http_headers[].value`| `server_headers`  | Where `http_response.http_headers[].name` = "Server Headers"                                                |                                                               |
| `observables[].value`               | `username`        | Where `observables[].type_id` = "4"                                                                         | Username if basic-auth is performed for the request.                                    |

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
| `unmapped`                        | `if_none_match`          |                                                               |
| `unmapped`                        | `if_modified_since`      |                                                               |
