# Event Dossier: Windows Security 4688
### Windows Security 4688 (A new process has been created)
- **Event Code**: 4688
- **Event Title**: A new process has been created
- **Description**: Translates Windows classic-formatted event 4688 (A new process has been created) to OCSF.
- **Event References**:
  - https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4688
  - https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4688
  
 ### OCSF Version: 0.31.2
 - `category_uid`: `1` `(System Activity)`
 - `class_uid`: `1007` `(Process Activity)`
 - `activity_id`: `1` `(Launch)`
 - `metadata.profiles`: `[host]`
 ### Mapping:
 
| OCSF                       | Raw                                                                                                                      |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `actor.process.file`       | `Process Information.Creator Process Name`                                                                               |
| `actor.process.pid`        | `Process Information.Creator Process ID`                                                                                 |
| `actor.user.domain`        | `Subject.Account Domain` *(MSFT event version 0-1)*<br>_OR_<br>`Creator Subject.Account Domain` *(MSFT event version 2)* |
| `actor.user.name`          | `Subject.Account Name` *(MSFT event version 0-1)*<br>_OR_<br>`Creator Subject.Account Name` *(MSFT event version 2)*     |
| `actor.user.session_uid`   | `Subject.Logon ID` *(MSFT event version 0-1)*<br>_OR_<br>`Creator Subject.Logon ID` *(MSFT event version 2)*             |
| `actor.user.uid`           | `Subject.Security ID` *(MSFT event version 0-1)*<br>_OR_<br>`Creator Subject.Security ID` *(MSFT event version 2)*       |
| `device.name`              | `ComputerName`                                                                                                           |
| `message`                  | `Message`                                                                                                                |
| `process.cmd_line`         | `Process Information.Process Command Line`                                                                               |
| `process.file`             | `Process Information.New Process Name`                                                                                   |
| `process.pid`              | `Process Information.New Process ID`                                                                                     |
| `process.user.domain`      | `Target Subject.Account Domain`                                                                                          |
| `process.user.name`        | `Target Subject.Account Name`                                                                                            |
| `process.user.session_uid` | `Target Subject.Logon ID`                                                                                                |
| `process.user.uid`         | `Target Subject.Security ID`                                                                                             |
