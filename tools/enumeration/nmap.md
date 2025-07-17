# NMap

## External

### Full Scan:

```
sudo nmap -sS -Pn -sV --open -iL targets.txt -p- -vv --min-hostgroup 255 --initial-rtt-timeout 150ms --max-rtt-timeout 300ms --max-scan-delay 0 -oA FULL
```

### UDP:

```
sudo nmap -Pn -sU -iL targets.txt -p 1-1024,5353,1900 -vvv | grep "/open" | awk '{ print $2 }' > UDP.txt
```

### LDAP:

```
sudo nmap --open -p 389 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt
```

### HTTP:

```
sudo nmap --open -p 80 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 80.txt
```

### HTTPS:

```
sudo nmap --open -p 443 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt
```

### Alt HTTP:

```
sudo nmap --open -p 8080 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 8080.txt
```

### Alt HTTPS:

```
sudo nmap --open -p 8443 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 8443.txt
```

### FTP:

```
sudo nmap --open -p 21 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt
```

### SSH:

```
sudo nmap --open -p 22 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt
```

### RDP:

```
sudo nmap --open -p 3389 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt
```

### All-in-One Scan - This takes longer&#x20;

```
sudo nmap --open -p 389 -iL targets.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt && sudo nma
```

## Internal

### Online Hosts(ICMP):

```
sudo nmap -sn -iL targets.txt -oG - | grep Up | cut -d' ' -f2 > up-hosts.txt
```

### Scan online hosts for common ports (21,22,80,389,443,3389,8443,8080, and UDP ports)

```
sudo nmap --open -p 389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt && sudo nmap --open -p 80 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 80.txt && sudo nmap --open -p 8080 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8080.txt && sudo nmap --open -p 443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt && sudo nmap --open -p 8443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8443.txt && sudo nmap --open -p 21 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt && sudo nmap --open -p 22 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt && sudo nmap --open -p 3389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt && sudo nmap --open -p 445 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 445.txt && sudo nmap -Pn -sU -iL up-hosts.txt -p 1-1024,5353,1900 -vvv | grep "/open" | awk '{ print $2 }' > UDP.txt
```

### Scan for shares that allow anonymous login

```
sudo nmap -p 445 --script smb-enum-shares.nse,smb-enum-users.nse -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > SMB-Anonymous-Shares.txt
```

### Find Domain Controller IP (typically works)

```
sudo nmap --open -p 389,88 -sV -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > DC-IP.txt
```

### Find if FTP Anonymous login in enabled

```
sudo nmap -p 21 --script ftp-anon -iL 21.txt
```

### SSH Authention Methods

```
sudo nmap -p 22 --script ssh-auth-methods --script-args="ssh.user=user" -iL 22.txt
```

### SNMP Info

```
nmap -Pn -sV -p 161 --script=snmp-info IP
```

### Full Scan

```
sudo nmap -sS -Pn -sV --open -iL targets.txt -p- -vv --min-hostgroup 255 --initial-rtt-timeout 150ms --max-rtt-timeout 300ms --max-scan-delay 0 -oA FULL
```

### LDAP

```
sudo nmap --open -p 389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt
```

### HTTP

```
sudo nmap --open -p 80 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 80.txt
```

### Alt HTTP

```
sudo nmap --open -p 8080 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8080.txt
```

### HTTPS

```
sudo nmap --open -p 443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt
```

### Alt HTTPS

```
sudo nmap --open -p 8443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 8443.txt
```

### FTP

```
sudo nmap --open -p 21 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt
```

### SMB

```
sudo nmap --open -p 139 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 139.txt
sudo nmap --open -p 445 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 445.txt
```

### Determine Which hosts don't have signing

```
sudo nmap --script=smb2-security-mode.nse -p 445 -iL up-hosts.txt relay.txt
```

### SSH

```
sudo nmap --open -p 22 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt
```

### RDP

```
sudo nmap --open -p 3389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt
```

