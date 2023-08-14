CERT/NetSA at CMU - SEI : SiLK Network Flow Record
==================================================

Translates a SiLK Network Flow Record to OCSF.


Reference: https://tools.netsa.cert.org/silk/


| OCSF | SiLK | default-values | Description / Comments |
| ---- | ---- | -------------- | ---------------------- |
| activity_name |  | Traffic | static mapping |
| activity_id |  | 6 | static mapping |
| category_uid |  | 4 | static mapping |
| category_name |  | Network Activity | static mapping |
| class_uid |  | 4001 | static mapping |
| class_name |  | Network Activity | static mapping |
| type_uid |  | 400106 | static mapping |
| type_name |  | Network Activity: Traffic |  |
|  |  |  |  |
| metadata.version |  | 1.0.0-rc.3 | OCSF version |
|  |  |  |  |
| metadata.product.name |  | SILK | static mapping |
| metadata.product.feature.name |  |  Network Flow Data | static mapping |
| metadata.product.vendor_name |  | CERT/NetSA at Carnegie Mellon University - Software Engineering Institute | static mapping |
| metadata.product.version | fileinfo. silk-version         |  |  |
|  |  |  |  |
| severity |  |  Informational | static mapping |
| severity_id |  | 1 | static mapping |
|  |  |  |  |
| src_endpoint.ip | sIP |  |  source IP address for flow in either IPV4 or IPV6 |
| dst_endpoint.ip | dIP |  |  destination IP address for flow |
| src_endpoint .port | sPort |  |  source port for flow (or 0) |
| dst_endpoint.port | dPort |  |  destination port for flow (or 0) |
| network_connection.protocol_num | protocol |  |  Transport layer protocol number for flow |
|  |  |  |   |
|  |  |  |   |
| network_traffic.packets | packets |  |  Number of packets in flow |
| network_traffic.bytes | bytes |  |  Number of bytes in flow (starting with IP header) |
| network_connection.tcp_flags | flags |  |  Cumulative TCP fag fields of flow (or blank)  |
| start_time | sTime |  |  Start date and time of flow  |
| duration | duration |  |  Duration of flow  |
| end_time | eTime |  |  End date and time of flow  |
| unmapped.sensor | sensor |  |  Sensor that collected the flow, example: S1 |
| unmapped.in | in |  |  Ingress interface or VLAN on sensor (usually 0)  |
| unmapped.out | out |  |  Egress interface or VLAN on sensor (usually 0)  |
| unmapped.nhIP | nhIP |  |  next hop IP address (Usually 0), example: 0.0.0.0 |
| unmapped.initialFlags | initialFlags |  |  TCP Flags in intial packets  |
| unmapped.sessionFlags | sessionFlags |  |  TCP Flags in remaining packets  |
| unmapped.attributes | attributes |  |  Termination Conditions |
| unmapped.application | application |  | Standard port of the application that produced the flow |
| unmapped.class | class |  |  class of sensor that collected the flow, example: all |
| network_connection.direction_id | type | (in, inweb, inicmp, innull) - 1; (out, outweb, outicmp, outnull) - 2; (int2int) - 3; (ext2ext, other) - 99 |  Type of flow for this sensor |
| network_connection.direction |  | (in, inweb, inicmp, innull) - Inbound; (out, outweb, outicmp, outnull) - Outbound; (int2int) - Lateral; (ext2ext, other) - Other |   |
| network_connection.boundary_id |  | (int2int) - 1; (ext2ext) - 3; (in, inweb, inicmp, innull) - 99; (out, outweb, outicmp, outnull) - 99; (other) - 99 |   |
| network_connection.boundary |  | (int2int) - Internal; (ext2ext) - External; (in, inweb, inicmp, innull) - other; (out, outweb, outicmp, outnull) - other; (other) - other |   |
| unmapped.iType | iType |  |  ICMP Type |
| unmapped.iCode | iCode |  |  ICMP code |
