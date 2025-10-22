# About
A tool to perform Kerberos pre-auth bruteforcing
## Links
[Github](https://github.com/ropnop/kerbrute)
[Releases](https://github.com/ropnop/kerbrute/releases)
# Installing
Get the most recent file from the [Releases Page](https://github.com/ropnop/kerbrute/releases) and make it executable
```
chmod +x kerbrute_linux_amd64
```
# Usage
```
./kerbrute -h
```
## User Enumeration
```
./kerbrute_linux_amd64 userenum -d DOMAIN --dc DC-IP USERLIST.txt -v -o Outfile.txt
./kerbrute_linux_amd64 userenum -d DOMAIN --dc DC-IP USERLIST.txt | grep "VALID USERNAME" | awk '{print $7}' > valid_users.txt
```
![[Pasted image 20250909132517.png]]
## PasswordSpray
```
./kerbrute_linux_amd64 passwordspray -d DOMAIN --dc DC-IP domain_users.txt PASSWORD -v -o Outfile.txt
```
![[Pasted image 20250909132521.png]]
## Bruteforce
```
./kerbrute_linux_amd64 bruteuser -d DOMAIN --dc DC-IP WORDLIST USER -v -o Outfile.txt
```
![[Pasted image 20250909132524.png]]