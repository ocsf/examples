# Event Dossier: Zeek http.log
### Summary:
- **Description**: Translates a Zeek http.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/http_activity
  - https://docs.zeek.org/en/master/logs/http.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/http/main.zeek.html#type-HTTP::Info
    
 ### Static mapping: OCSF Version 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `HTTP Activity`
 - `class_uid`: `4002`
 - `metadata.log_name`: `http.log`
 - `metadata.loggers.log_provider`: `Zeek`
 - `metadata.loggers.product.name=`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `http.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/http.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:

| OCSF                           | Raw               |
| ------------------------------ | ----------------- |
|`time`                          |`ts`               |
|`start_time`                    |`ts`               |
|`metadata.logged_time`          |`_write_ts`        |
|`metadata.loggers[].name`       |`_system_name`     |
|`metadata.uid`                  |`uid`              |
|`src_endpoint.ip`               |`id.orig_h`        |
|`src_endpoint.port`             |`id.orig_p`        |
|`dst_endpoint.ip`               |`id.resp_h`        |
|`dst_endpoint.port`             |`id.resp_p`        |
|`http_request.http_cookies.value` |`cookie`         |
|`http_request.http_headers.name`  |"Accept Language"|
|`http_request.http_headers.value` |`accept_language`|
|`http_request.http_headers.name`  |"Accept Encoding"| 
|`http_request.http_headers.value` |`accept_encoding`|
|`http_request.http_headers.name`  |"Accept"         |
|`http_request.http_headers.value` |`accept`         |
|`http_request.http_headers.name`  |"Body"           |
|`http_request.http_headers.value` |`post_body`      |
|`http_request.http_headers.name`  |"Origin"         |
|`http_request.http_headers.value` |`origin`         |
|`http_request.http_headers.name`  |"Client Headers" |
|`http_request.http_headers.value` |`client_headers` |
|`http_request.http_method`      |`method`           |
|`http_request.length`           |`request_body_len` |
|`http_request.referrer`         |`referrer`         |
|`http_request.url.hostname`     |`dest_host`        |
|`http_request.url.path`         |`uri`              |
|`http_request.user_agent`       |`user_agent`       |
|`http_request.version`          |`version`          |
|`http_request.x_forwarded_for`  |`proxied`          |
|`http_response.code`            |`status_code`      |
|`http_response.http_cookies.value` |`resp_cookie`   |
|`http_response.http_headers.value` |`server_headers`|
|`http_response.length`          |`response_body_len`|
|`http_response.status`          |`status_msg`       |
|`message`                       |`tags`             |
|`observables.type_id:21`        |`username`         |


 ### Unmapped (proposed):
 
| OCSF                     | Raw                      |
| -------------------------| -------------------------|
| `file.name (src)`        | `orig_filenames`         |
| `file.name (dst)`        | `resp_filenames`         |
| `file.mime_type (src)`   | `orig_mime_types`        |
| `file.mime_type (dst)`   | `resp_mime_types`        |
| `file.uid (src)`         | `orig_fuids`             |
| `file.uid (dst)`         | `resp_fuids`             |
| `unmapped`               | `trans_depth`            |
| `unmapped`               | `if_none_match`          |
| `unmapped`               | `if_modified_since`      |
