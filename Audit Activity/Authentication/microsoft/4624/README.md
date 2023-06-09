# Event Dossier: Windows Security 4624
### Windows Security 4624 (An account was successfully logged on)
- **Event Code**: 4624
- **Event Title**: An account was successfully logged on
- **Description**: Translates Windows classic-formatted event 4624 (An account was successfully logged on) to OCSF.
- **Event References**:
  - https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4624
  - https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624
  
 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `3` `(System Activity)`
 - `class_uid`: `3002` `(Process Activity)`
 - `activity_id`: `1` `(Logon)`
 - `metadata.profiles`: `[host]`
 ### Mapping:
 
| OCSF                     | Raw                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `actor.process.file`     | `Process Information.Process Name`                                                                          |
| `actor.process.pid`      | `Process Information.Process ID`                                                                            |
| `actor.user.domain`      | `Subject.Account Domain`                                                                                    |
| `actor.user.name`        | `Subject.Account Name`                                                                                      |
| `actor.user.session_uid` | `Subject.Logon ID`                                                                                          |
| `actor.user.uid`         | `Subject.Security ID`                                                                                       |
| `auth_protocol`          | `Detailed Authentication Information.Authentication Package`                                                |
| `device.name`            | `ComputerName`                                                                                              |
| `dst_endpoint.hostname`  | `ComputerName`                                                                                              |                                                                                                  |
| `logon_process.name`     | `Detailed Authentication Information.Logon Process`                                                         |
| `logon_type_id`          | `Logon Type` *(MSFT event version 0-1)*<br>_OR_<br> `Logon Information.Logon Type` *(MSFT event version 2)* |
| `message`                | `Message` 
| `src_endpoint.name`      | `Network Information.Workstation Name`                                                                      |
