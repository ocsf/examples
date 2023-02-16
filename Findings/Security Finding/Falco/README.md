# Event Dossier: Falco
## Falco Alert
- **Description**: Translates a Falco alert to OCSF. 
- **Event References**:
  - https://falco.org/docs/alerts/channels/#json-output

## OCSF Version: 0.33.0
 - `activity_id`: `1` (`Generate`)
 - `category_uid`: `2` `(Findings)`
 - `class_uid`: `2001` `(Security Finding)`
 - `metadata.product.name`: `Falco`
 - `metadata.product.vendor_name`: `Falcosecurity`

## Mapping:
 - This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

| OCSF                   | Raw        |
| ---------------------- | ---------- |
| `finding.created_time` | `time`     |
| `finding.desc`         | `output`   |
| `finding.title`        | `rule`     |
| `finding.types`        | `source`   |
| `finding.uid`          | `uuid`     |
| `metadata.labels`      | `tags`     |
| `status`               | `priority` |
