# Event Dossier: Zeek http.log
### 
- **Description**: Translates a Zeek http.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/http_activity
  - https://docs.zeek.org/en/master/logs/http.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/http/main.zeek.html#type-http::Info
    
 ### OCSF Version: 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `HTTP Activity`
 - `class_uid`: `4002`
 - `metadata.log_name`: `http.log`
 - `metadata.loggers.log_provider`: `Zeek`
 - `metadata.loggers.product.name=`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `rdp.log`
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
|`metadata.loggers.logged_time`  |`_write_ts`        |
|`metadata.loggers.name`         |`_system_name`     |
|`metadata.uid`                  |`uid`              |
|`src_endpoint.ip`               |`id.orig_h`        |
|`src_endpoint.port`             |`id.orig_p`        |
|`dst_endpoint.ip`               |`id.resp_h`        |
|`dst_endpoint.port`             |`id.resp_p`        |
|`email.message_uid`             |`msg_id`           |
|`email.from`                    |`from`             |
|`email.to`                      |`to`               |
|`email.smtp_to`                 |`rcptto`           |
|`email.smtp_from`               |`mailfrom`         |
|`email_url_activity.url.hostname` |`domains`        |
|`email_url_activity.url.url_string` |`urls`         |
|`network_activity.proxy.intermediate_ips` |`path`   |
|`network_file_activity.file.uid`|`fuids`            |
|`smtp_hello`                    |`helo`             |
|`status_detail`                 |`last_reply`       |

 ### Unmapped fields:
 
| OCSF                     | Raw                      |
| -------------------------| -------------------------|
| `unmapped`               | `date`                   |
| `unmapped`               | `tls`                    |
| `(app_name)`             | `is_webmail`             | 		
