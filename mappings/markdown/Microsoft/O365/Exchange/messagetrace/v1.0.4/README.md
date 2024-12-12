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
