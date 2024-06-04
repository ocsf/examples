# Event Dossier: Windows Security 4625
### Windows Security 4625 (An account failed to log on)
- **Event Code**: 4625
- **Event Title**: An account failed to log on
- **Description**: Translates Windows classic-formatted event 4625 (An account failed to log on) to OCSF.
- **Event References**:
  - https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4625
  - https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4625
  
 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `3` `(System Activity)`
 - `class_uid`: `3002` `(Process Activity)`
 - `activity_id`: `1` `(Logon)`
 - `metadata.profiles`: `[host]`
 ### Mapping:
 
| OCSF                     | Raw                                                          |
| ------------------------ | ------------------------------------------------------------ |
| `actor.process.file`     | `Process Information.Caller Process Name`                    |
| `actor.process.pid`      | `Process Information.Caller Process ID`                      |
| `actor.user.domain`      | `Subject.Account Domain`                                     |
| `actor.user.name`        | `Subject.Account Name`                                       |
| `actor.user.session_uid` | `Subject.Logon ID`                                           |
| `actor.user.uid`         | `Subject.Security ID`                                        |
| `auth_protocol`          | `Detailed Authentication Information.Authentication Package` |
| `device.name`            | `ComputerName`                                               |
| `dst_endpoint.hostname`  | `ComputerName`                                               |
| `logon_process.name`     | `Detailed Authentication Information.Logon Process`          |
| `logon_type_id`          | `Logon Type`                                                 |
| `message`                | `Message`                                                    |
| `src_endpoint.ip`        | `Source Network Address`                                     |
| `src_endpoint.name`      | `Network Information.Workstation Name`                       |
| `src_endpoint.port`      | `Source Port`                                                |
| `status`                 | `Failure Information.Status`                                 |
| `status_detail`          | `Failure Information.Failure Reason`                         |
| `status_id`              | `2`                                                          |
| `user.domain`            | `Account For Which Logon Failed.Account Domain`              |
| `user.name`              | `Account For Which Logon Failed.Security ID`                 |
| `user.uid`               | `Failure Information.Status`                                 |
