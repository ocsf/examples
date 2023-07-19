# Event Dossier: Zeek dns.log
### NOERROR Query Results
- **Description**: Translates a Zeek query log to OCSF. 
- **Event References**:
  - https://docs.zeek.org/en/master/logs/dns.html
  - https://schema.ocsf.io/1.0.0-rc.3/objects/dns_query
  
 ### OCSF Version: 1.0.0-rc.3
 - `category_uid`: `4`
 - `category_name`: `Network Activity`
 - `class_uid`: `4003`
 - `class_name`: `DNS Activity`
 - `metadata.profiles`: `[security_control]`
 - `metadata.product.name`: `Zeek`
 - `metadata.product.feature.name`: `dns.log`
 - `metadata.product.vendor_name`: `Zeek`
 - `severity`: `Informational`
 - `severity_id`: `1`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

 - Any field not present in an explicit mapping will be moved to the unmapped object.

| OCSF                          | Raw             |
| ----------------------------- | --------------- |
|'time'                         |'ts'             |
|'metadata.uid'                 |'uid'            |
|'src_endpoint.ip'              |'id.orig_h'      |
|'src_endpoint.port'            |'id.orig_p'      |
|'query.hostname'               |'query'          |
|'query.type'                   |'qtype_name'     |
|'query.class'                  |'qclass_name'    |
|'rcode'                        |'rcode_name'     |
|'rcode_id'                     |'rcode_name'     |
|'answers.rdata'                 |'answers'        |
|'dst_endpoint.ip'              |'id.resp_h'      |
|'dst_endpoint.port'            |'id.resp_p'      |
|'connection_info.protocol_name'|'proto'          |
|'answers.ttl'                  |'TTLs            |
|'answers.packet_uid'           |'trans_id'       |
|'activity_id':'4'              |'reject'         |
| ----------------------------- | --------------- |

 ### Conditional Mapping:
 - Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

### Notes regarding DNS Flags:
AA (Authoritative Answer): This flag indicates if the DNS server believes the response is from an authoritative source for the specific domain. If "AA" is set to "true", this would indicate that the response is coming from a server that has authority over the queried domain. In your case, it's set to "false", which means the server doesn't claim authority over the queried domain.

TC (TrunCation): This flag indicates if the message was truncated because it was too long for the UDP transmission. If the message exceeds the maximum size (usually 512 bytes for UDP), it will be truncated and this flag will be set to "true". In your case, it's "false", which means the message wasn't truncated.

RD (Recursion Desired): This flag indicates if the client (i.e., the system making the request) wants the server to perform recursion to resolve a query. Recursion involves the server querying other DNS servers on behalf of the client. Here it's "true", so the client requested recursion.

RA (Recursion Available): This flag indicates if the DNS server can perform recursive queries. If it's "true", the server can perform recursion. Here it's "false", which means that the server does not have the capability to perform recursion.

Z (Reserved for future use): This field is reserved for future use. In current DNS specifications, it should always be "0" in all queries and responses.


| OCSF                       | Raw           | 
| -------------------------- | ------------- |
|'answers.flag_ids':`1`       |'AA'           | 
|'answers.flag_ids':`2`       |'TC'           | 
|'answers.flag_ids':`3`       |'RD'           | 
|'answers.flag_ids':`4`       |'RA'           | 
|'answers.flag_ids':`99`      |'Z'            |
| -------------------------- | ------------- |


 ### Unmapped:
| OCSF                       | Raw           |
| -------------------------- | ------------- |
|'unmapped'                  |'rtt'          |
|'unmapped'                  |'unmapped'     |
| -------------------------- | ------------- |
