# Defense

## Windows Defense & Event Log Reference

> Defensive/detection companion to the offense notes: the Windows event IDs that matter for spotting the activity described elsewhere, what each one means, and which log it lives in. Use it two ways - as a **blue-team** detection reference, and as a **red-team** "what am I lighting up?" checklist.
>
> Companion files: **Windows-Offense.md** (the commands/tradecraft that generate these events) and **Active Directory (AD).md** (the concepts behind the account, group, and authentication events).
>
> Primary external reference: the [Ultimate Windows Security Log Encyclopedia](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/),\
> which has a detailed page per event ID (each ID below links to it).

***

### How to read this

Windows writes an event every time something security-relevant happens - a logon,\
a new process, a service install, a cleared log. Each event has a numeric **Event**\
**ID**, a **log** it's written to, and a set of fields. Defenders build detections\
by alerting on specific IDs (and field values); attackers care about the same IDs\
because they are the trail their actions leave behind.

A few things to keep in mind:

* **An event ID alone is rarely a verdict.** Event **4624** (successful logon)\
  fires thousands of times a day on a busy host; what makes it interesting is the\
  _&#x4C;ogon Type_, the _source IP_, the _account_, and the _time_. The IDs below are\
  starting points for a detection, not the detection itself.
* **Logon Type matters.** Several auth events are annotated below with the\
  relevant types - most often **Type 3** (network, e.g. SMB/share access, a huge\
  share of lateral-movement traffic) and **Type 10** (RemoteInteractive, i.e.\
  RDP). Other common types: 2 (interactive/at the keyboard), 4 (batch/scheduled\
  task), 5 (service), 7 (unlock), 8 (network cleartext), 9 (new credentials, e.g.\
  `runas /netonly`).
* **Many of these require audit policy to be enabled.** Process-creation logging\
  (**4688**) and, especially, command-line capture in 4688 are **off by default**\
  and must be turned on via Group Policy. The same is true for object-access\
  auditing (**4663/4660**) and others. Absence of an event doesn't prove the\
  action didn't happen - it may just not be audited.

### Where these events live (log sources)

Not everything is in the Security log. Knowing the source tells you where to point\
your collection/queries.

| Event IDs                | Log / source                                                                                  |
| ------------------------ | --------------------------------------------------------------------------------------------- |
| `46xx`, `47xx`, `1102`   | **Security** (`Windows Logs → Security`)                                                      |
| `70xx` (service control) | **System** (Service Control Manager)                                                          |
| `2003` (firewall)        | **Microsoft-Windows-Windows Firewall With Advanced Security/Firewall**                        |
| `80xx` (AppLocker)       | **Microsoft-Windows-AppLocker/\*** (EXE and DLL, MSI and Script, etc.)                        |
| USB-related IDs          | **System**, plus **Microsoft-Windows-DriverFrameworks-UserMode** and related operational logs |

> **Sysmon** (Sysinternals) is the common force-multiplier here: its **Event ID 1**\
> captures richer process-creation detail than 4688, **3** network connections,\
> **7** image/DLL loads, **11** file creation, **13** registry edits, and more.\
> It's a separate log (`Microsoft-Windows-Sysmon/Operational`) and must be\
> installed, but it's worth knowing that the offense activity in\
> **Windows-Offense.md** is usually _more_ visible with Sysmon than with the\
> stock Security log.

### Account & group management

Creating accounts, resetting passwords, and slipping a user into a privileged\
group are classic **persistence** and **privilege-escalation** footprints. A new\
account followed immediately by a group addition is a high-signal sequence.

| Event                                               | ID                                                                                               | Why it matters                                                                                  |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| User account created                                | [4720](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4720) | New account - a common persistence move. Watch for creation outside normal provisioning.        |
| User account enabled                                | [4722](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4722) | A disabled (e.g. dormant/former-employee) account being switched back on.                       |
| Attempt to reset an account's password              | [4724](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4724) | Admin-style password reset of another account - possible account takeover.                      |
| User account deleted                                | [4726](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4726) | Account removal - can be cleanup/anti-forensics after misuse.                                   |
| Member added to a security-enabled **global** group | [4728](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4728) | e.g. adding a user to **Domain Admins**. High-value alert.                                      |
| Member added to a security-enabled **local** group  | [4732](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4732) | e.g. adding a user to the local **Administrators** group on a host.                             |
| User account locked out                             | [4740](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4740) | Lockout - a burst of these can indicate **password spraying / brute force**.                    |
| User account unlocked                               | [4767](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4767) | Account unlocked - note who unlocked it and whether it correlates with 4740.                    |
| Permissions on an object were changed               | [4670](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4670) | ACL/DACL change - relevant to **ACL-abuse** persistence (e.g. granting rights on an AD object). |

> See **Active Directory (AD).md → Default Security Groups** for _which_ groups\
> (Domain Admins, Enterprise Admins, etc.) make a 4728/4732 genuinely alarming.

### Authentication & logon

The most voluminous - and most attacked - events. Lateral movement, pass-the-hash,\
and RDP hijacking all leave marks here.

| Event                                  | ID                                                                                               | Why it matters                                                                                                                                                                                                                  |
| -------------------------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Logon success                          | [4624](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4624) | The core "who logged on where" event. **Type 3** = network (SMB/shares, lateral movement); **Type 10** = RDP. Pivot on account, source IP, and time.                                                                            |
| Logon failed                           | [4625](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4625) | Failed logons. Volume + pattern reveals **brute force / spraying**; the Logon Type and Status/Sub-Status codes say _why_ it failed.                                                                                             |
| User-initiated logoff                  | [4647](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4647) | Clean logoff initiated by the user; useful for session timelining.                                                                                                                                                              |
| NTLM credential validation on the DC   | [4776](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4776) | The DC attempted to validate an account's credentials over **NTLM**. A spike of 4776 failures is a strong **NTLM brute-force / spray** signal; also relevant to **pass-the-hash** (NTLM auth where Kerberos would be expected). |
| Terminal Services session reconnected  | [4778](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4778) | An RDP/console session was **reconnected** (includes client name/IP) - part of RDP session tracking and **session-hijack** detection.                                                                                           |
| Terminal Services session disconnected | [4779](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4779) | An RDP/console session was **disconnected** (see Corrections - the source table mislabeled this as "Reconnected").                                                                                                              |

> **Kerberos vs. NTLM:** seeing **4776** (NTLM) for an account that normally\
> authenticates via Kerberos can indicate pass-the-hash or a downgrade. For the\
> protocol background, see **Active Directory (AD).md → Authentication: NTLM and**\
> **Kerberos**. (Kerberos TGT/TGS events - 4768/4769/4771 - aren't in the source\
> table but are the natural next additions for Kerberoasting/AS-REP detection.)

### Process execution

| Event               | ID                                                                                               | Why it matters                                                                                                                                                                                                                                                                                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| New process created | [4688](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4688) | Every process start. With **command-line auditing enabled**, this captures the full command line - which is how the "stealthy launcher" (`powershell.exe -NoP -NonI -W Hidden -Exec Bypass -Enc <base64>`) in **Windows-Offense.md** gets recorded despite the hidden window. Pair with **PowerShell script-block logging (4104)** for decoded `-Enc` payloads. |

> 4688 command-line capture and PowerShell 4104 script-block logging are the two\
> settings that most reduce an attacker's ability to hide PowerShell activity.\
> Both are off by default.

### Object access & DCSync

Auditing reads/writes/deletes on specific objects (files, directory objects).\
Noisy unless scoped, but essential for catching **credential theft from AD**.

| Event                                                     | ID                                                                                               | Why it matters                                                                                                                                                                                                                                                                                                                                                |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| An attempt was made to access an object                   | [4663](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4663) | An actual access attempt on an audited object (requires SACL auditing). The access-mask tells you read vs. write vs. delete.                                                                                                                                                                                                                                  |
| A handle to an object was requested with intent to delete | [4659](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4659) | Delete intent on an audited object.                                                                                                                                                                                                                                                                                                                           |
| An object was deleted                                     | [4660](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4660) | The deletion itself (pairs with the 4663/4659 handle event).                                                                                                                                                                                                                                                                                                  |
| Directory-service / DCSync-style access                   | [4662](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4662) | An operation on an AD object. **The key DCSync tell:** a 4662 referencing the replication extended rights GUIDs (`DS-Replication-Get-Changes` / `-All`, `1131f6aa-…` / `1131f6ad-…`) from a non-DC account means someone is pulling password hashes via replication. See **Active Directory (AD).md → The AD DS Data Store** for why `NTDS.dit` is the prize. |

> **DCSync** is the headline detection here: a normal domain member should never\
> request directory replication. Alerting on **4662 + the replication GUIDs from a**\
> **non-DC principal** is one of the highest-value AD detections you can build.

### Services

Installing or reconfiguring a service is a long-standing mechanism for\
**persistence**, **privilege escalation** (service runs as SYSTEM), and\
**lateral execution** (e.g. remote service creation like PsExec).

| Event                                 | ID                                                                                               | Log      | Why it matters                                                                                                                          |
| ------------------------------------- | ------------------------------------------------------------------------------------------------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| A service was installed in the system | [4697](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4697) | Security | Service install recorded in the **Security** log (needs audit policy). High-signal for PsExec-style tooling.                            |
| A new service was created             | 7045                                                                                             | System   | The **System**-log counterpart (Service Control Manager). 7045 is the classic PsExec/remote-service IOC.                                |
| Service install (SCM)                 | 7030                                                                                             | System   | Service reported it could not be started as configured (e.g. interactive service) - can surface oddly-configured implants.              |
| Service terminated unexpectedly       | 7034                                                                                             | System   | A service crashed/was killed - can indicate tampering with a security service.                                                          |
| Service start type changed            | 7040                                                                                             | System   | Start type flipped between **disabled / manual / automatic** - e.g. disabling a defensive service, or setting an implant to auto-start. |
| Service was started or stopped        | 7036                                                                                             | System   | Routine but useful for correlating the start/stop of a security product (AV/EDR) or a suspicious service.                               |

### AppLocker

AppLocker enforces which executables, scripts, installers, and DLLs are allowed to\
run. Its events tell you both about **blocked** attacker tooling and about what\
_&#x77;ould_ have been blocked in audit mode.

| Event IDs | Meaning                                                                   |
| --------- | ------------------------------------------------------------------------- |
| 8003      | File **allowed but would have been blocked** (audit-only mode) - EXE/DLL. |
| 8004      | File **blocked** from running - EXE/DLL.                                  |
| 8006      | Script/MSI **would have been blocked** (audit-only mode).                 |
| 8007      | Script/MSI **blocked**.                                                   |

> 8004/8007 (hard blocks) are direct evidence a defense stopped something; 8003/8006\
> (audit) are a goldmine for tuning - they show exactly what an attacker ran that a\
> future enforcement rule should catch.

### Defense evasion & log tampering

The events that fire when someone tries to blind the defenders. These are\
inherently high-signal - legitimate admins rarely clear logs or disable the\
firewall ad hoc.

| Event                                       | ID                                                                                               | Log      | Why it matters                                                                                                                 |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------ | -------- | ------------------------------------------------------------------------------------------------------------------------------ |
| The audit log was cleared                   | [1102](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=1102) | Security | **Clearing the Security log.** Almost always worth an alert - a hallmark of anti-forensics. (System-log clears raise **104**.) |
| Windows Firewall setting changed / disabled | 2003                                                                                             | Firewall | Firewall being turned off or a protection setting changed - common pre-step to lateral movement or C2.                         |

### Removable media (USB insertion)

USB insertion doesn't map to a single clean ID; it scatters across the System log\
and several driver/USB operational logs. Treat this as a _cluster_ to correlate\
rather than one authoritative event. Relevant IDs seen on insertion:

| IDs                 | Source / meaning                                                                                                       |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 7045                | A **driver/service** gets installed for a newly-attached device (same ID as service creation - context disambiguates). |
| 10000, 10001, 10100 | Device configuration / driver-install lifecycle (DriverFrameworks-UserMode / UMDF).                                    |
| 20001, 20003        | Device install / plug-and-play completion (see Corrections - the source listed `20001` twice).                         |
| 24576, 24577, 24579 | USB/mass-storage mount and related lifecycle events.                                                                   |

> For serious USB/data-exfil monitoring, these event logs are usually combined\
> with registry forensics (`USBSTOR`, `MountedDevices`) rather than relied on\
> alone.

### Corrections applied

While consolidating `Event Codes.md` into this file, two errors in the original\
table were fixed; they're called out here so the change is traceable:

* **4779** was labeled "Terminal Service Session Reconnected" (a duplicate of\
  **4778**). 4779 is the **disconnected** event; 4778 is reconnected. Corrected\
  above.
* The USB row listed **`20001, 20001, 20003`** - `20001` was duplicated. Recorded\
  as **`20001, 20003`** above.
