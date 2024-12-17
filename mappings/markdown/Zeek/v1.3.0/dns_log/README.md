# Event Dossier: Zeek dns.log
### Summary:
- **Description**: Translates a Zeek dns.log to OCSF. 
- **Event References**:
  - https://schema.ocsf.io/1.3.0/classes/dns_activity
  - https://docs.zeek.org/en/master/logs/dns.html
  - https://docs.zeek.org/en/current/scripts/base/protocols/dns/main.zeek.html

 ### OCSF Version: v1.3.0


 ### Static value mapping:
| OCSF field                          | Value        | Type       |
| ----------------------------------- | ------------ | ---------- |
| `metadata.version`                  | "1.3.0"      |            |
| `category_uid`                      | 4            | Integer    |
| `class_uid`                         | 4003         | Integer    |
| `severity_id`                       | 1            | Integer    |
| `metadata.product.name`             | "Zeek"       |            |
| `metadata.product.vendor_name`      | "Zeek"       |            |


 ### Direct field mapping:
| OCSF                          | Raw                         | Zeek Field Description                                                      | Notes                   |
| ----------------------------- | --------------------------- | --------------------------------------------------------------------------- | ----------------------- |
| `time`                        | `ts`                        | Timestamp indicating when the event occurred.                               | Convert to epoch value. <br>Type is timestamp_t (Integer). |
| `start_time`                  | `ts`                        | Timestamp indicating when the event occurred.                               | Convert to epoch value. <br>Type is timestamp_t (Integer). |
| `metadata.logged_time`        | `_write_ts`                 | Timestamp indicating when the log entry was written to disk.                | Convert to epoch value. <br>Type is timestamp_t (Integer). |
| `metadata.loggers[].name`     | `_system_name`              | Name of the system or logging subsystem generating the log entry.           |                         |
| `metadata.log_name`           | `_path`                     | Log name.                                                                   |                         |
| `metadata.uid`                | `uid`                       | Unique ID for the connection.                                               |                         |
| `src_endpoint.ip`             | `id.orig_h`     | The originator’s IP address.                                                            | Type is ip_t.           |
| `src_endpoint.port`           | `id.orig_p`     | The originator’s port number.                                                           | Type is port_t (Integer). |
| `dst_endpoint.ip`             | `id.resp_h`     | The responder’s IP address.                                                             | Type is ip_t.           |
| `dst_endpoint.port`           | `id.resp_p`     | The responder’s port number.                                                            | Type is port_t (Integer). |
| `connection_info.protocol_name`| `proto`        | The transport layer protocol of the connection.                                         |                         |
| `query.hostname`              | `query`         | The domain name that is the subject of the DNS query.                                   |                         |
| `query.type`                  | `qtype_name`    | A descriptive name for the type of the query.                                           |                         |
| `query.class`                 | `qclass_name`   | A descriptive name for the class of the query.                                          |                         |
| `rcode`                       | `rcode_name`    | A descriptive name for the response code value.                                         |                         |
| `rcode_id`                    | `rcode`         | The response code value in DNS response messages.                                       | Type is Integer.        |
| `response_time`               | `rtt`           | Round trip time for the query and response.                                             | Type is timestamp_t (Integer). |
| `answers[].rdata`             | `answers`       | The set of resource descriptions in the query answer.                                   |                         |
| `answers[].ttl`               | `TTLs`          | The caching intervals of the associated RRs described by the answers field.             | Type is Integer.        |
| `answers[].packet_uid`        | `trans_id`      | A 16-bit identifier assigned by the program that generated the DNS query.               | Type is Integer.        |
| `query.packet_uid`            | `trans_id`      | A 16-bit identifier assigned by the program that generated the DNS query.               | Type is Integer.        |


 ### Conditional mapping:
Fields described here are subject to dynamic mappings contingent on a conditional evaluation of source data.
| OCSF                          | Raw             | Evaluation Conditions           | Zeek Field Description                                                                 | Notes |
| ----------------------------- | --------------- | ------------------------------- | ---------------------------------------------------------------------------------------| --------- |
| `answers[].flag_ids[]`            | `AA`            | If `AA` = "true", "1". | The Authoritative Answer bit for response messages specifies that the responding name server is an authority for the domain. | AA (Authoritative Answer): This flag indicates if the DNS server believes the response is from an authoritative source for the specific domain. If "AA" is set to "true", this would indicate that the response is coming from a server that has authority over the queried domain. In your case, it's set to "false", which means the server doesn't claim authority over the queried domain. Type is Integer. |
| `answers[].flag_ids[]`            | `TC`            | If `TC` = "true", "2". | The Truncation bit specifies that the message was truncated.                           | TC (TrunCation): This flag indicates if the message was truncated because it was too long for the UDP transmission. If the message exceeds the maximum size (usually 512 bytes for UDP), it will be truncated and this flag will be set to "true". In your case, it's "false", which means the message wasn't truncated. Type is Integer. |
| `answers[].flag_ids[]`            | `RD`            | If `RD` = "true", "3". | The Recursion Desired bit in a request message indicates that the client wants recursive service for this query. | RD (Recursion Desired): This flag indicates if the client (i.e., the system making the request) wants the server to perform recursion to resolve a query. Recursion involves the server querying other DNS servers on behalf of the client. Here it's "true", so the client requested recursion. Type is Integer. |
| `answers[].flag_ids[]`            | `RA`            | If `RA` = "true", "4". | The Recursion Available bit in a response message indicates that the name server supports recursive queries. | RA (Recursion Available): This flag indicates if the DNS server can perform recursive queries. If it's "true", the server can perform recursion. Here it's "false", which means that the server does not have the capability to perform recursion. Type is Integer. |
| `answers[].flag_ids[]`            | `Z`             | If `Z` = "true", "99" <br>and `answers[].flags[]` = "DNSSEC Flag". | A reserved field that is zero in queries and responses unless using DNSSEC.            | Z (Reserved for future use): This field is reserved for future use. In current DNS specifications, it should always be "0" in all queries and responses. Type is Integer. |
| `status_id`                   | `rejected`      | If `rejected` = "false", "1" <br>if `rejected` = "true", "2" <br>else "0". | The DNS query was rejected by the server. Type is Integer. |


 ### Unmapped:
| OCSF                       | Raw                       | Zeek Field Description                          |
| -------------------------- | ------------------------- | ----------------------------------------------- |
| `unmapped`                 | `icann_host_subdomain`    |                                                 |
| `unmapped`                 | `icann_domain`            |                                                 |
| `unmapped`                 | `icann_tld`               |                                                 |
| `unmapped`                 | `is_trusted_domain`       |                                                 |
| `unmapped`                 | `qclass`                  | The QCLASS value specifying the class of the query. |
| `unmapped`                 | `qtype`                   | A QTYPE value specifying the type of the query. |
