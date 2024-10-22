# Event Dossier: Zeek dns.log
### NOERROR Query Results
- **Description**: Translates a Zeek query log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/dns_activity
  - https://docs.zeek.org/en/master/logs/dns.html
  - https://docs.zeek.org/en/current/scripts/base/protocols/dns/main.zeek.html
    
 ### OCSF Version: 1.3.0
 - `metadata.version`: `1.3.0`
 - `category_name`: `Network Activity`
 - `category_uid`: `4`
 - `class_name`: `DNS Activity`
 - `class_uid`: `4003`
 - `metadata.log_name`: `dns.log`
 - `metadata.loggers.log_provider`: `Zeek`
 - `metadata.loggers.product.name=`: `Zeek`
 - `metadata.product.cpe_name`: `cpe:2.3:a:zeek:zeek`
 - `metadata.product.feature.name`: `dns.log`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.url_string`: `https://docs.zeek.org/en/current/logs/dns.html`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any field not present in an explicit mapping will be moved to the unmapped object.

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
|`connection_info.protocol_name`|`proto`          |
|`query.hostname`               |`query`          |
|`query.type`                   |`qtype_name`     |
|`query.class`                  |`qclass_name`    |
|`rcode`                        |`rcode_name`     |
|`rcode_id`                     |`rcode`          |
|`response_time`                |`rtt`            |
|`activity_id`:`4`              |`rejected`       |
|`answers.rdata`                |`answers`        |
|`answers.ttl`                  |`TTLs`           |
|`answers.flag_ids.1`           |`AA`             | 
|`answers.flag_ids.2`           |`TC`             | 
|`answers.flag_ids.3`           |`RD`             | 
|`answers.flag_ids.4`           |`RA`             | 
|`answers.flag_ids.99`          |`Z`              |
|`answers.packet_uid`           |`trans_id`       |
|`query.packet_uid`             |`trans_id`       |

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

### Notes regarding DNS Flags:
AA (Authoritative Answer): This flag indicates if the DNS server believes the response is from an authoritative source for the specific domain. If "AA" is set to "true", this would indicate that the response is coming from a server that has authority over the queried domain. In your case, it's set to "false", which means the server doesn't claim authority over the queried domain.

TC (TrunCation): This flag indicates if the message was truncated because it was too long for the UDP transmission. If the message exceeds the maximum size (usually 512 bytes for UDP), it will be truncated and this flag will be set to "true". In your case, it's "false", which means the message wasn't truncated.

RD (Recursion Desired): This flag indicates if the client (i.e., the system making the request) wants the server to perform recursion to resolve a query. Recursion involves the server querying other DNS servers on behalf of the client. Here it's "true", so the client requested recursion.

RA (Recursion Available): This flag indicates if the DNS server can perform recursive queries. If it's "true", the server can perform recursion. Here it's "false", which means that the server does not have the capability to perform recursion.

Z (Reserved for future use): This field is reserved for future use. In current DNS specifications, it should always be "0" in all queries and responses.

 ### Unmapped:
| OCSF                       | Raw                       |
| -------------------------- | ------------------------- |
|`unmapped`                  |`icann_host_subdomain`     |
|`unmapped`                  |`icann_domain`             |
|`unmapped`                  |`icann_tld`                |
|`unmapped`                  |`is_trusted_domain`        |
|`unmapped`                  |`qclass`                   |
|`unmapped`                  |`qtype`                    |
