# Event Dossier: Zeek rdp.log
### Summary:
- **Description**: Translates a Zeek rdp.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/rdp_activity
  - https://docs.zeek.org/en/master/logs/rdp.html
  - https://docs.zeek.org/en/master/scripts/base/protocols/rdp/main.zeek.html#type-RDP::Info
    
 ### Static mapping: OCSF Version: 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `RDP Activity`
 - `class_uid`: `4007`
 - `metadata.log_name`: `rdp.log`
 - `metadata.loggers.log_provider`: `Zeek`
 - `metadata.loggers.product.name=`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `rdp.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/rdp.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`
 - `dst_endpoint.agent_list.type`: `Remote Access`
 - `dst_endpoint.agent_list.type_id`: `9`
 - `src_endpoint.agent_list.type`: `Remote Access`
 - `src_endpoint.agent_list.type_id`: `9`

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
|`src_endpoint.hostname`         |`client_name`      |
|`src_endpoint.agent_list.name`  |`client_build`     |
|`src_endpoint.agent_list.version`|`client_dig_product_id`|   
|`dst_endpoint.ip`               |`id.resp_h`        |
|`dst_endpoint.port`             |`id.resp_p`        |
|`identifier_cookie`             |`cookie`           |
|`protocol_ver`                  |`security_protocol`|
|`status_detail`                 |`result`           |
|`tls.key_length`                |`encryption_method`|
|`observable.type_id:30`         |`rdfp_hash`        |
|`observable.type_id:99`         |`rdfp_string`      |
|`observables.type_id:99`        |`keyboard_layout`  |
|`remote_display.color_depth`    |`requested_color_depth`|
|`remote_display.physical_height`|`desktop_height`     |
|`remote_display.physical_width` |`desktop_width`      |

 ### Unmapped:
 
| OCSF                     | Raw                      |
| -------------------------| -------------------------|
|`unmapped`                      |`cert_count`        |
|`unmapped`                      |`cert_permanent`    |
|`unmapped`                      |`cert_type`         |
|`unmapped`                      |`channels_joined`   |
|`unmapped`                      |`client_channels`   |
|`unmapped`                      |`encryption_level`  |
