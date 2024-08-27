# Event Dossier: Microsoft Defender Antivirus MALWAREPROTECTION_STATE_MALWARE_DETECTED/1116
###  The antimalware platform detected malware or other potentially unwanted software.
- **Event (Code/ID/Name)**: 1116
- **Event Title**: The antimalware platform detected malware or other potentially unwanted software.
- **Description**:"Translates Windows Defender Antivirus event 1116 to a OCSF Detection Finding"
- **Event References**:
  - https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-microsoft-defender-antivirus

 ### OCSF Version: 1.2.0
 - category_uid: 2 (Findings)
 - class_uid: 2004 (Detection Findings)
 - activity_id: 1 (Create)

 ### Detection Finding Mapping:
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `time`                   | `Event.System.Detection Time`                                                                               |
| `severity`               | `Event.EventData.Severity Name`                                                                             |
| `severity_id`            | `Event.EventData.Severity ID`                                                                               |
| `status_code`            | `Event.EventData.Status Code`                                                                               |
| `status_detail`          | `Event.EventData.Status Description`                                                                        |


 ### Findings Information Mapping:
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `title`                  | `Event.EventData.Threat Name`                                                                               |
| `uid`                    | `Event.EventData.Detection ID`                                                                              |
| `types`                  | `Event.Category ID`                                                                                         |


### Evidence Artifact Mapping:
## File
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `type_id`                | `1`                                                                                                         |
| `name`                   | `Path.file:_`                                                                                               |

## Process
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `name`                   | `Event.EventData.Process Name`                                                                              |
| `pid`                    | `Path.process:_ pid:_`                                                                                      |

## Container
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `name`                   | `Path.Containerfile:_`                                                                                      |

## Actor
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `user.name`              | `System.EventData.Detection User`                                                                           |

                                 
### Remmediation Mapping:
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `desc`                   | `Event.EventData.Additional Actions String`                                                                 |
| `references`             | `Event.EventData.FWLink`                                                                                    |

### Metadata Mapping:                                                                                                       
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `event_uid`              | `Event.System.EventRecordID`                                                                                |
| `event_code`             | `Event.System.EventID`                                                                                      |
| `log_level`              | `Event.System.Level`                                                                                        |
| `log_provider`           | `Event.System.Provider Name`                                                                                |
| `log_version`            | `Event.System.Version`                                                                                      |
| `logged_time`            | `Event.System.TimeCreated SystemTime`                                                                       |
| `product`                | `Event.EventData.Product Name`                                                                              |