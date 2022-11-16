# Event Dossier: Windows Security 4688
### Windows Security 4688 (A new process has been created)
- **Event Code**: 4688
- **Event Title**: A new process has been created
- **Description**: Translates Windows classic-formatted event 4688 (A new process has been created) to OCSF.
- **Event References**:
  - https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4688
  - https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4688
  
 ### Mapping:
 
| OCSF        | Raw           |
| ------------- |-------------|
| actor.process.file       | Process Information.Creator Process Name |
| actor.process.pid        | Process Information.Creator Process ID   |
| process.cmd_line         | Process Information.Process Command Line |
| process.file             | Process Information.New Process Name     |
| process.pid              | Process Information.New Process ID       |
| process.user.domain      | Target Subject.Account Domain            |
| process.user.name        | Target Subject.Account Name              |
| process.user.session_uid | Target Subject.Logon ID                  |
| process.user.uid         | Target Subject.Security ID               |
