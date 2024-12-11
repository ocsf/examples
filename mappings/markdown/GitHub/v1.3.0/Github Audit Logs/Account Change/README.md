# Event Dossier: Github audit log Account Change

### A Github audit log for

- **Description**: Translates a `user.create` log to OCSF.
- **Event References**:
  - https://docs.github.com/en/enterprise-cloud@latest/admin/monitoring-activity-in-your-enterprise/reviewing-audit-logs-for-your-enterprise/audit-log-events-for-your-enterprise#business

### OCSF Version: 1.3.0

- `class_name`: `Account Change`
- `class_uid`: `3001`
- `category_name`: `Identity & Access Management`
- `category_uid`: `3`
- `severity_id`: `1`
- `severity`: `Informational`
- `metadata.product.name`: `Github Audit Log`
- `metadata.product.vendor_name`: `Github`
- `metadata.profiles`: `[datetime, host]`
- `metadata.version`: `1.3.0`

### Mapping:

- This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

Any fields not present in an explicit mapping will be mapped to the unmapped object.

| OCSF                                | Raw                          |
| ----------------------------------- | ---------------------------- |
| `actor.user.name`                   | `actor`                      |
| `actor.user.uid`                    | `actor_id`                   |
| `actor.session.uid`                 | `actor_session`              |
| `metadata.event_code`               | `action`                     |
| `time`                              | `@timestamp`                 |
| `http_request.user_agent`           | `user_agent`                 |
| `http_request.url.url_string`       | `url`                        |
| `metadata.uid`                      | `_document_id`                |
| `http_request.referrer`             | `referrer`                   |
| `http_request.http_method`          | `method`                     |
| `src_endpoint.ip`                   | `actor_ip`                   |
| `src_endpoint.location.city`        | `actor_location.city`        |
| `src_endpoint.location.country`     | `actor_location.country`     |
| `src_endpoint.location.postal_code` | `actor_location.postal_code` |
| `user.name`                         | `user`                       |
| `user.uid`                          | `user_id`                    |

### Conditional Mapping:

- Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                        | Raw                     |
| --------------------------- | ----------------------- |
| `activity_name/activity_id` | `action/operation_type` |
