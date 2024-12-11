# Event Dossier: Github audit log Authentication

### A Github audit log for

- **Description**: Translates a `business.sso_response` log to OCSF.
- **Event References**:
  - https://docs.github.com/en/enterprise-cloud@latest/admin/monitoring-activity-in-your-enterprise/reviewing-audit-logs-for-your-enterprise/audit-log-events-for-your-enterprise#business

### OCSF Version: 1.3.0

- `class_name`: `Authentication`
- `class_uid`: `3002`
- `category_name`: `Identity & Access Management`
- `category_uid`: `3`
- `severity_id`: `1`
- `metadata.product.name`: `Github Audit Log`
- `metadata.product.vendor_name`: `Github`
- `metadata.profiles`: `[datetime, host]`
- `metadata.version`: `1.3.0`

### Mapping:

- This does not reflect any transformations or evaluations of the data. Some data evaluation and transformation will be necessary for a correct representation in OCSF that matches all requirements.

Any fields not present in an explicit mapping will be mapped to the unmapped object.

| OCSF                                | Raw                           |
| ----------------------------------- | ----------------------------- |
| `actor.user.name`                   | `actor`                       |
| `actor.user.uid`                    | `actor_id`                    |
| `actor.session.uid`                 | `actor_session`               |
| `actor.user.email_addr`             | `external_identity_nameid`    |
| `actor.session.issuer`              | `issuer`                      |
| `metadata.event_code`               | `action`                      |
| `metadata.uid`                      | `_document_id`                |
| `time`                              | `@timestamp`                  |
| `http_request.user_agent`           | `user_agent`                  |
| `http_request.referrer`             | `referrer`                    |
| `src_endpoint.ip`                   | `actor_ip`                    |
| `src_endpoint.location.city`        | `actor_location.city`         |
| `src_endpoint.location.country`     | `actor_location.country_code` |
| `src_endpoint.location.postal_code` | `actor_location.postal_code`  |
| `user.name`                         | `user`                        |
| `user.uid`                          | `user_id`                     |

### Conditional Mapping:

- Any fields described within the conditional mappings are subject to dynamic mappings contingent on a conditional evaluation of source data. Fields which fail to meet a particular conditional are assigned a default value from the OCSF schema description.

| OCSF                        | Raw                     |
| --------------------------- | ----------------------- |
| `activity_name/activity_id` | `action/operation_type` |
| `auth_protocol`             | `action`                |
