# Event Dossier: IBM QRadar SIEM
### IBM QRadar SIEM Offense
- **Description**: IBM® QRadar® uses rules to monitor the events and flows in your network to detect security threats. When the events and flows meet the test criteria that is defined in the rules, an offense is created to show that a security attack or policy breach is suspected.
- **Event References**:
  - https://ibmsecuritydocs.github.io/qradar_api_19.0/19.0--siem-offenses-GET.html
  - https://ibmsecuritydocs.github.io/qradar_api_19.0/19.0--siem-source_addresses-source_address_id-GET.html
  - https://ibmsecuritydocs.github.io/qradar_api_19.0/19.0--siem-local_destination_addresses-local_destination_address_id-GET.html
  - https://ibmsecuritydocs.github.io/qradar_api_19.0/19.0--analytics-rules-id-GET.html

 ### OCSF Version: 1.0.0
 - `category_uid` : `2`
 - `category_name` : `Findings`
 - `class_uid` : `2001`
 - `class_name` : `Security Finding`
 - `metadata.product.name` : `QRadar SIEM`
 - `metadata.product.vendor_name` : `IBM`
 - `metadata.product.version` : `7.5.0`
 - `metadata.product.lang` : `en`
 - `metadata.log_name` : `Offense`
 - `metadata.log_provider` : `IBM QRadar`

 ### Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

#### offense
| OCSF                       | Raw             |
| -------------------------- | ----------------|
| `activity_id` | `convert(offense.status, offense.close_time, offense.first_persisted_time, offense.last_persisted_time)` |
| `activity_name` | `convert(offense.status, offense.close_time, offense.first_persisted_time, offense.last_persisted_time)` |
| `status_code` | `offense.status` |
| `state` | `convert(offense.status, offense.close_time, offense.first_persisted_time, offense.last_persisted_time)` |
| `time` | `offense.start_time` |
| `message` | `offense.description` |
| `end_time` | `offense.last_persisted_time` |
| `count` | `(offense.event_count + offense.flow_count)` |
| `metadata.original_time` | `offense.start_time` |
| `metadata.modified_time` | `offense.last_updated_time` |
| `finding.uid` | `offense.id` |
| `finding.created_time` | `offense.start_time` |
| `finding.first_seen_time` | `offense.first_persisted_time` |
| `finding.last_seen_time` | `offense.last_persisted_time` |
| `finding.desc` | `offense.description` |
| `finding.title` | `offense.description` |
| `analytic.name` | `CRE` |
| `analytic.name` | `Custom Rule Engine` |
| `analytic.type` | `Rule` |
| `analytic.type_id` | `1` |
| `analytic.related_analytic[n].uid` | `offense.rules[n].id` |
| `analytic.related_analytic[n].name` | `rules.name(offense.rules[n].id)` |
| `analytic.related_analytic[n].category` | `offense.rules[n].type` |
| `analytic.related_analytic[n].type` | `Rule` |
| `analytic.related_analytic[n].type_id` | `1` |
| `risk_level_id` | `convert(offense.severity)` |
| `risk_level` | `convert(offense.severity)` |
| `impact_id` | `convert(offense.relevance)` |
| `impact` | `convert(offense.relevance)` |
| `confidence_id` | `convert(offense.credibility)` |
| `confidence` | `convert(offense.credibility)` |
| `enrichment.magnitude` | `offense.magnitude` |
| `enrichment.category_count` | `offense.category_count` |
| `enrichment.device_count` | `offense.device_count` |
| `enrichment.event_count` | `offense.event_count` |
| `enrichment.flow_count` | `offense.flow_count` |
| `enrichment.policy_category_count` | `offense.policy_category_count` |
| `enrichment.remote_destination_count` | `offense.remote_destination_count` |
| `enrichment.local_destination_count` | `offense.local_destination_count` |
| `enrichment.security_category_count` | `offense.security_category_count` |
| `enrichment.source_count` | `offense.source_count` |
| `enrichment.username_count` | `offense.username_count` |
| `enrichment.offense_type` | `offense.offense_type` |
| `enrichment.offense_source` | `offense.offense_source` |
| `enrichment.domain_id` | `offense.domain_id` |
| `enrichment.destination_network` | `offense.destination_networks[n]` |
| `enrichment.source_network>` | `offense.source_network` |
| `enrichment.closing_reason_id>` | `offense.closing_reason_id` |
| `enrichment.close_time` | `offense.close_time` |
| `data_sources[n]` | `offense.log_sources[n].name` |
| `observable.(Other).log_source_id` | `offense.log_sources[n].id` |
| `observable.(Other).log_source_name` | `offense.log_sources[n].name` |
| `observable.(Other).log_source_type_id` | `offense.log_sources[n].type_id` |
| `observable.(Other).log_source_type_name` | `offense.log_sources[n].type_name` |
| `observable.(User).assigned_to` | `offense.assigned_to` |
| `observable.(User).closing_user` | `offense.closing_user` |
| `observable.(IP Address).source_address_ids[n]` | `source_addresses.source_address_id(source_address_ids[n])` |
| `observable.(IP Address).local_destination_address_ids[n]` | `local_destination_addresses.local_destination_address_id(local_destination_address_ids[n])` |
| `observable.(Other).low_level_category[n]` | `offense.categories[n]` |
| `malware.classifications[n]` | `convert(offense.categories[n])` |
| `malware.classification_ids[n]` | `convert(offense.categories[n])` |

