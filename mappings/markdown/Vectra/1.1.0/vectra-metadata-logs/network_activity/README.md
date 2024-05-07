# Event Dossier: Vectra Metadata Logs to OCSF class Network Activity

## wip: provided mapping files are not validated against schema server yet so required fields might be missing
---
* Class name: `network_activity`
* Vendor name: `vectra`
* Product name: `vectra-metadata-logs`
* Event codes: `METADATA_TYPE = 'metadata_isession'`
---

| OCSF | RAW |
| --- | --- |
| action | ```CASE (0::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Allowed' WHEN 2 THEN 'Denied' WHEN 99 THEN 'Other' END``` |
| action_id | ```0::NUMBER``` |
| activity_id | ```CASE WHEN RAW:conn_state = 'S1' THEN 1 WHEN RAW:conn_state = 'RSTO' THEN 2 WHEN RAW:conn_state = 'RSTR' THEN 3 WHEN RAW:conn_state = 's2' THEN 4 WHEN RAW:conn_state = 'REJ' THEN 5 WHEN RAW:conn_state = 'OTH' THEN 6 ELSE 99 END::NUMBER``` |
| activity_name | ```CASE (CASE WHEN RAW:conn_state = 'S1' THEN 1 WHEN RAW:conn_state = 'RSTO' THEN 2 WHEN RAW:conn_state = 'RSTR' THEN 3 WHEN RAW:conn_state = 's2' THEN 4 WHEN RAW:conn_state = 'REJ' THEN 5 WHEN RAW:conn_state = 'OTH' THEN 6 ELSE 99 END::NUMBER) WHEN 0 THEN 'Unknown' WHEN 1 THEN 'Open' WHEN 2 THEN 'Close' WHEN 3 THEN 'Reset' WHEN 4 THEN 'Fail' WHEN 5 THEN 'Refuse' WHEN 6 THEN 'Traffic' WHEN 99 THEN 'Other' END``` |
| actor.user.name | ```USERNAME::VARCHAR``` |
| category_name | ```CASE (4::NUMBER) WHEN 4 THEN 'Network Activity' END``` |
| category_uid | ```4::NUMBER``` |
| class_name | ```'network_activity'``` |
| class_uid | ```4001``` |
| connection_info.protocol_name | ```PROTO_NAME::VARCHAR``` |
| connection_info.protocol_num | ```PROTO::NUMBER``` |
| device.hostname | ```HOSTNAME::VARCHAR``` |
| dst_endpoint.domain | ```RESP_DOMAINS::VARCHAR``` |
| dst_endpoint.hostname | ```RESP_HOSTNAME::VARCHAR``` |
| dst_endpoint.ip | ```COALESCE(ID_RESP_H, ASSIGNED_IP)::VARCHAR``` |
| dst_endpoint.uid | ```RESP_HUID::VARCHAR``` |
| dst_endpoint.vlan_uid | ```RAW:resp_vlan_id::VARCHAR``` |
| metadata.event_code | ```METADATA_TYPE``` |
| metadata.product.name | ```'vectra-metadata-logs'``` |
| metadata.product.vendor_name | ```'vectra'``` |
| metadata.tenant_uid | ```UID::VARCHAR``` |
| metadata.version | ```'1.1.0'``` |
| src_endpoint.hostname | ```ORIG_HOSTNAME::VARCHAR``` |
| src_endpoint.ip | ```ID_ORIG_H::VARCHAR``` |
| src_endpoint.mac | ```MAC::VARCHAR``` |
| src_endpoint.port | ```ID_ORIG_P::VARCHAR``` |
| src_endpoint.uid | ```ORIG_HUID::VARCHAR``` |
| src_endpoint.vlan_uid | ```RAW:orig_vlan_id::VARCHAR``` |
| start_time | ```date_part('epoch_milliseconds', EVENT_TIME::TIMESTAMP_LTZ)``` |
| start_time_dt | ```EVENT_TIME::TIMESTAMP_LTZ``` |
| time | ```date_part('epoch_milliseconds', event_time::TIMESTAMP_LTZ)``` |
| time_dt | ```event_time::TIMESTAMP_LTZ``` |
| tls.alert | ```TTLS::NUMBER``` |
| traffic.bytes_in | ```RAW:resp_ip_bytes::NUMBER``` |
| traffic.bytes_out | ```RAW:orig_ip_bytes::NUMBER``` |
| traffic.packets_in | ```RAW:resp_pkts::NUMBER``` |
| traffic.packets_out | ```RAW:orig_pkts::NUMBER``` |
| type_name | ```CASE (CASE WHEN RAW:conn_state = 'S1' THEN 400101 WHEN RAW:conn_state = 'RSTO' THEN 400102 WHEN RAW:conn_state = 'RSTR' THEN 400103 WHEN RAW:conn_state = 's2' THEN 400104 WHEN RAW:conn_state = 'REJ' THEN 400105 WHEN RAW:conn_state = 'OTH' THEN 400106 ELSE 400199 END) WHEN 400100 THEN 'Network Activity: Unknown' WHEN 400101 THEN 'Network Activity: Open' WHEN 400102 THEN 'Network Activity: Close' WHEN 400103 THEN 'Network Activity: Reset' WHEN 400104 THEN 'Network Activity: Fail' WHEN 400105 THEN 'Network Activity: Refuse' WHEN 400106 THEN 'Network Activity: Traffic' WHEN 400199 THEN 'Network Activity: Other' END``` |
| type_uid | ```CASE WHEN RAW:conn_state = 'S1' THEN 400101 WHEN RAW:conn_state = 'RSTO' THEN 400102 WHEN RAW:conn_state = 'RSTR' THEN 400103 WHEN RAW:conn_state = 's2' THEN 400104 WHEN RAW:conn_state = 'REJ' THEN 400105 WHEN RAW:conn_state = 'OTH' THEN 400106 ELSE 400199 END``` |

Contributed to the OCSF community by [Hunters](https://www.hunters.security/) with ❤
