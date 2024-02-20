# Event Dossier: Windows Security 4689
### Windows Security 4689 (A process has exited)
- **Event Code**: 4689
- **Event Title**: A process has exited
- **Description**: Translates Windows classic-formatted event 4689 (A process has exited) to OCSF.
- **Event References**:
  - https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4689
  - https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4689
  
 ### OCSF Version: 1.0.0-rc.2
 - `category_uid`: `1` `(System Activity)`
 - `class_uid`: `1007` `(Process Activity)`
 - `activity_id`: `2` `(Terminate)`
 - `metadata.profiles`: `[host]`
 ### Mapping:
 
| OCSF                     | Raw                                |
| ------------------------ | ---------------------------------- |
| `actor.process.file`     | `Process Information.Process Name` |
| `actor.user.domain`      | `Subject.Account Domain`           |
| `actor.user.name`        | `Subject.Account Name`             |
| `actor.user.session_uid` | `Subject.Logon ID`                 |
| `actor.user.uid`         | `Subject.Security ID`              |
| `device.name`            | `ComputerName`                     |
| `message`                | `Message`                          |
| `process.file`           | `Process Information.Process Name` |
| `process.pid`            | `Process Information.Process ID`   |
| `process.user.domain`    | `Target Subject.Account Domain`    |
