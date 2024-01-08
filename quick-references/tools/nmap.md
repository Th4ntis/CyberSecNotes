# NMap

## NMap

### Full Scan:

```
sudo nmap -sS -Pn -sV --open -iL targets.txt -p- -vv --min-hostgroup 255 --initial-rtt-timeout 150ms --max-rtt-timeout 300ms --max-scan-delay 0 -oA FULL 
```

### Online Hosts:

```
sudo nmap -sn -iL safe-nets.txt -oG - | grep Up | cut -d' ' -f2 > up-hosts.txt 
```

### UDP:

```
sudo nmap -Pn -sU -iL targets.txt -p 1-1024,5353,1900 -vvv -oA UDP 
```

### ICMP:

```
sudo nmap -sn -iL targets.txt -oG - | grep Up | cut -d' ' -f2 > up-hosts.txt 
```

### LDAP:

```
sudo nmap --open -p 389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 389.txt 
```

### SMB:

```
sudo nmap --open -p 443 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 443.txt 
```

### RDP:

```
sudo nmap --open -p 3389 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 3389.txt 

If Open:
nmap -p 3389 --script rdp-ntlm-info <targets>
```

### FTP:

```
sudo nmap --open -p 21 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 21.txt 
```

### SSH:

```
sudo nmap --open -p 22 -iL up-hosts.txt -oG - | grep "/open" | awk '{ print $2 }' > 22.txt 
```
