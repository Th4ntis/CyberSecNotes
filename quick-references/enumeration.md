# Enumeration

## Web directory

```bash
gobuster dir --url http://(ip) -w (wordlist)
```

## SMB

List directories

```bash
smbclient -L (ip)
```

## Crackmap

List users if Guest account is enabled

```bash
crackmapexec smb (ip) -u 'Guest' -p '' --rid-brute
```
