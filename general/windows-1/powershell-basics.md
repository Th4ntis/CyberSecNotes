# Powershell Basics

Microsoft has a free course on Introduction to Powershell [here](https://docs.microsoft.com/en-us/learn/modules/introduction-to-powershell/) on their website. Information on [about\_Powershell.exe](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about\_powershell\_exe?view=powershell-5.1\&viewFallbackFrom=powershell-7.2).

We can run powershell from the Start Menu by searching for it, through the command prompt by running `powershell.exe`, or through the run dialogbox(`windows key+r`) and running `powershell.exe`

### Cmdlet

A cmdlet is a lightweight command that is used in the PowerShell environment. The PowerShell runtime invokes these cmdlets within the context of automation scripts that are provided at the command line. Cmdlets perform an action and typically return a Microsoft .NET object to the next command in the pipeline. A cmdlet is a single command that participates in the pipeline semantics of PowerShell. This includes binary (C#) cmdlets, advanced script functions, CDXML, and Workflows.

## Commands

* `IEX` OR `Invoke Expression`
  * The `Invoke-Expression` cmdlet evaluates or runs a specified string as a command and returns the results of the expression or command. Without `Invoke-Expression`, a string submitted at the command line is returned (echoed) unchanged.

### Download files:

*   Invoke-WebRequest http://`(IP)`:(PORT)/(FILE) -Outfile (Outputfile)

    * Invoke-WebRequest -URI http://192.168.1.52:8000/test.txt -Outfile Downloaded.txt



![](<../../.gitbook/assets/image (113).png>)

* "IEX (New-Object Net.WebClient).DownloadString('URL')"
  * IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.52:8000/test.txt')

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
