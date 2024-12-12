# Event Dossier: Microsoft Office 365 Exchange Messagetrace
### Summary
- **Description**: Translates Microsoft MessageTrace report to OCSF. 

- **Event References**:
  - https://learn.microsoft.com/en-us/previous-versions/office/developer/o365-enterprise-developers/jj984335(v=office.15)
  - https://github.com/MicrosoftDocs/office-docs-powershell/blob/main/exchange/exchange-ps/exchange/Get-MessageTrace.md
 
 ### OCSF Version: 1.0.4

 ### Static mapping:
| OCSF field                          | Value                                           |
| ----------------------------------- | ----------------------------------------------- |
| `activity_id`                       | `4`                                             |
| `activity_name`                     | `Trace`                                         |
| `category_name`                     | `Network Activity`                              |
| `category_uid`                      | `4`                                             |
| `class_name`                        | `Email Activity`                                |
| `class_uid`                         | `4009`                                          |
| `metadata.product.name`             | `O365`                                          |
| `metadata.product.vendor_name`      | `Microsoft`                                     | 
| `metadata.version`                  | `1.4.0`                                         |
| `direction_id`                      | `0`                                             |
| `direction_name`                    | `Unknown`                                       |
| `severity`                          | `Unknown`                                       |
| `severity_id`                       | `0`                                             |

 ### Mapping:

| OCSF                           | Raw                             |
| ------------------------------ | ------------------------------- |
| `email.message_uid`            | `MessageId`                     |
| `email.size`                   | `Size`                          |
| `email.smtp_from`              | `SenderAddress`                 |
| `email.smtp_to`                | `RecipientAddress`              |
| `email.subject`                | `Subject`                       |
| `message_trace_uid`            | `MessageTraceId`                |
| `metadata.original_time`       | `Received`                      |
| `src_endpoint.ip`              | `FromIP`                        |
| `status_detail`                | `Status`                        |
| `time`                         | `Received` (converted to epoch) |

### Calculated Mapping
| OCSF                                | Calculation                               | Notes
| ----------------------------------- | ----------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `type_uid`                          | `class_uid * 100 + activity_id` (`400904`)| Given the simple calculation, implementers may either calculate this field or statically map it to 400904 |

### Conditional Mapping
| OCSF                           | Condition                                                                                         |
| ------------------------------ | ------------------------------------------------------------------------------------------------- |
| `status`                       | `default: "Unknown, if "Delivered": "Success", if "Failed": "Failure", else: value of raw Status` |
| `status_id`                    | `default: 0, if "Delivered": 1, if "Failed": 2, else: 99`                                         |

### Unmapped
| OCSF                           | Raw                             |
| ------------------------------ | ------------------------------- |
| `unmapped.Index`               | `Index`                         |
| `unmapped.Organization`        | `Organization`                  |