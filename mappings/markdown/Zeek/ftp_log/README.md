# Event Dossier: Zeek ftp.log
### Summary:
- **Description**: Translates a Zeek FTP log to OCSF. 
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
 - `metadata.loggers.log_provider`: `Zeek`
 - `metadata.loggers.product.name=`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `ftp.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/ftp.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:

| OCSF                          | Raw             |
| ----------------------------- | --------------- |
|`time`                         |`ts`             |
|`start_time`                   |`ts`             |
|`metadata.loggers.logged_time` |`_write_ts`      |
|`metadata.loggers.name`        |`_system_name`   |
|`metadata.uid`                 |`uid`            |
|`src_endpoint.ip`              |`id.orig_h`      |
|`src_endpoint.port`            |`id.orig_p`      |
|`dst_endpoint.ip`              |`id.resp_h`      |
|`dst_endpoint.port`            |`id.resp_p`      |
|`activity_id`                  |`data_channel.passive`|
|`file.size`                    |`file_size`      |
|`ftp_activity.command`         |`command` && `arg` |
|`ftp_activity.codes`           |`reply_code`     |
|`status_code`                  |`reply_code`     |
|`status_detailed`              |`reply_msg`      |
|`network_connection_info.direction`  |`data_channel.orig_h` && `data_channel.resp_h`|
|`observables.type_id:21`       |`user`           |
|`observables.type_id:21`       |`password`       |
