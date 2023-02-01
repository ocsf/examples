# Event Dossier: IBM QRadar SIEM
### IBM QRadar SIEM Offense
- **Description**: IBM® QRadar® uses rules to monitor the events and flows in your network to detect security threats. When the events and flows meet the test criteria that is defined in the rules, an offense is created to show that a security attack or policy breach is suspected.
- **Event References**:
  - https://ibmsecuritydocs.github.io/qradar_api_17.0/17.0--siem-offenses-GET.html

 ### OCSF Version: 1.0.0
 - `category_uid` : `2`
 - `category_name` : `Findings`
 - `class_uid` : `2001`
 - `class_name` : `Security Finding`
 - `metadata.product.name` : `QRadar SIEM`
 - `metadata.product.vendor_name` : `IBM`
 - `metadata.product.version` : `7.5.0`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

#### offense
| OCSF                       | Raw             |
| -------------------------- | ----------------|
| `metadata.original_time` | `start_time` |
| `metadata.modified_time` | `last_updated_time` |
| `finding.uid` | `id` |
| `finding.created_time` | `start_time` |
| `finding.first_seen_time` | `first_persisted_time` |
| `finding.last_seen_time` | `last_persisted_time` |
| `finding.desc` | `description` |
| `finding.title` | `description` |
| `enrichment.<CategoryCount>` | `category_count` |
| `enrichment.<DeviceCount>` | `device_count` |
| `enrichment.<EventCount>` | `event_count` |
| `enrichment.<FlowCount>` | `flow_count` |
| `enrichment.<PolicyCategoryCount>` | `policy_category_count` |
| `enrichment.<RemoteDestinationCount>` | `remote_destination_count` |
| `enrichment.<LocalDestinationCount>` | `local_destination_count` |
| `enrichment.<SecurityCategoryCount>` | `security_category_count` |
| `enrichment.<SourceCount>` | `source_count` |
| `enrichment.<UsernameCount>` | `username_count` |
| `enrichment.<Magnitude>` | `magnitude` |
| `enrichment.<Credibility>` | `credibility` |
| `enrichment.<Relevance>` | `relevance` |
| `enrichment.<Severity>` | `severity` |
| `enrichment.<OffenseType>` | `offense_type` |
| `enrichment.<OffenseSource>` | `offense_source` |
| `enrichment.<DomainID>` | `domain_id` |
| `enrichment.<Rule>` | `rules[n]` |
| `enrichment.<ClosingReasonId>` | `closing_reason_id` |
| `enrichment.<CloseTime>` | `close_time` |
| `time` | `start_time` |
| `message` | `description` |
| `end_time` | `last_persisted_time` |
| `severity_id` | `severity & magnitude` |
| `severity` | `severity & magnitude` |
| `observable.<AssignedTo(User)>` | `assigned_to` |
| `observable.<ClosingUser(User)>` | `closing_user` |
| `observable.<Category(Other)>` | `categories[n]` |
| `observable.<DestinationNetwork(Other)>` | `destination_networks[n]` |
| `observable.<LogSourceId(Other)>` | `log_sources[n].id` |
| `observable.<LogSourceName(Other)>` | `log_sources[n].name` |
| `observable.<LogSourceTypeId(Other)>` | `log_sources[n].type_id` |
| `observable.<LogSourceTypeName(Other)>` | `log_sources[n].type_name` |
| `observable.<DomainId(Other)>` | `domain_id` |
| `observable.<SourceAddress(IP Address)>` | `source_address_ids[n]` |
| `observable.<LocalDestinationAddress(IP Address)>` | `local_destination_address_ids[n]` |
| `status_code` | `status` |


