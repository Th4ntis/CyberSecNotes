# External
- Full Scan:
```
sudo nmap -sS -Pn -sV --open -iL targets.txt -p- -vv --min-hostgroup 255 --initial-rtt-timeout 150ms --max-rtt-timeout 300ms --max-scan-delay 0 -oA FULL
```
- UDP:
```
sudo nmap -Pn -sU -iL targets.txt -p 1-1024,5353,1900 -vvv | grep "/open" | awk '{ print $2 }' > UDP.txt
```
- LDAP:
```
sudo nmap --open -p 389 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt
```
- HTTP:
```
sudo nmap --open -p 80 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 80.txt
```
- HTTPS:
```
sudo nmap --open -p 443 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt
```
- Alt HTTP:
```
sudo nmap --open -p 8080 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 8080.txt
```
- Alt HTTPS:
```
sudo nmap --open -p 8443 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 8443.txt
```
- FTP:
```
sudo nmap --open -p 21 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt
```
- SSH:
```
sudo nmap --open -p 22 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt
```
- RDP:
```
sudo nmap --open -p 3389 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt
```
	- If RDP is open
```
sudo nmap -p 3389 --script rdp-ntlm-info -iL 3389.txt > RDP-NTLM-Info.txt
```
- All in one:
```
sudo nmap --open -p 389 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt && sudo nmap --open -p 80 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 80.txt && sudo nmap --open -p 8080 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 8080.txt && sudo nmap --open -p 443 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt && sudo nmap --open -p 8443 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 8443.txt && sudo nmap --open -p 21 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt && sudo nmap --open -p 22 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt && sudo nmap --open -p 3389 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt && sudo nmap -Pn -sU -iL targets.txt -p 1-1024,5353,1900 -vvv | grep "/open" | awk '{ print $2 }' > UDP.txt
```

# Internal
## Linux
- Full Scan:
```
sudo nmap -sS -Pn -sV --open -iL targets.txt -p- -vv --min-hostgroup 255 --initial-rtt-timeout 150ms --max-rtt-timeout 300ms --max-scan-delay 0 -oA FULL
```
- Online Hosts(ICMP):
```
sudo nmap -sn -iL targets.txt -oG - | grep Up | cut -d' ' -f2 > up-hosts.txt
```
- LDAP:
```
sudo nmap --open -p 389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt
```
- HTTP:
```
sudo nmap --open -p 80 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 80.txt
```
- Alt HTTP:
```
sudo nmap --open -p 8080 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8080.txt
```
- HTTPS:
```
sudo nmap --open -p 443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt
```
- Alt HTTPS:
```
sudo nmap --open -p 8443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8443.txt
```
- FTP:
```
sudo nmap --open -p 21 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt
```
- SMB
```
sudo nmap --open -p 139 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 139.txt
sudo nmap --open -p 445 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 445.txt
```
- Determine Which hosts don't have signing
```
sudo nmap --script=smb2-security-mode.nse -p 445 -iL up-hosts.txt relay.txt
```
- SSH:
```
sudo nmap --open -p 22 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt
```
- SMB
```
sudo nmap --open -p 445 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 445.txt
```
- RDP:
```
sudo nmap --open -p 3389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt
```
- If RDP is open
```
sudo nmap -p 3389 --script rdp-ntlm-info -iL 3389.txt > RDP-NTLM-Info.txt
```
- UDP:
```
sudo nmap -Pn -sU -iL targets.txt -p 1-1024,5353,1900 -vvv -oA UDP
sudo nmap -Pn -sU -iL up-hosts.txt -p 1-1024,5353,1900 -vvv | grep "/open" | awk '{ print $2 }' > UDP.txt
```
- Scan for shares that allow anonymous login
```
sudo nmap -p 445 --script smb-enum-shares.nse,smb-enum-users.nse -iL targets.txt
```

- All In one:
```
sudo nmap --open -p 389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt && sudo nmap --open -p 80 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 80.txt && sudo nmap --open -p 8080 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8080.txt && sudo nmap --open -p 443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt && sudo nmap --open -p 8443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8443.txt && sudo nmap --open -p 21 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt && sudo nmap --open -p 22 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt && sudo nmap --open -p 3389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt && sudo nmap --open -p 445 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 445.txt && sudo nmap -Pn -sU -iL up-hosts.txt -p 1-1024,5353,1900 -vvv | grep "/open" | awk '{ print $2 }' > UDP.txt
```

## Windows
- Find Uphosts:
```
nmap -sn 10.2.2.0/24 -oG - | ForEach-Object { if ($_ -match "Up$") { ($_ -split ' ')[1] } } > up-hosts.txt
nmap -sn -iL targets.txt -oG - | ForEach-Object { if ($_ -match "Up$") { ($_ -split ' ')[1] } } > up-hosts.txt
```
- Scan and output to file:
```
nmap -p 80 --open -iL targets.txt > 80.txt
```
- SMB Signing Not Required:
```
nmap -p 445 -iL uphosts.txt --script smb2-security-mode.nse > smb-signing-not-required.txt 
```
- SNMP Info (default community name)
```
nmap -Pn -sV -p 161 --script=snmp-info IP
```
- Puts saved output into just list of IPs:
```
Select-String -Path "input.txt" -Pattern '\b(?:\d{1,3}\.){3}\d{1,3}\b' | ForEach-Object { $_.Matches.Value } > output.txt
```