# About
A next generation version of enum4linux (a Windows/Samba enumeration tool) with additional features like JSON/YAML export. Aimed for security professionals and CTF players.

## Links
[Github](https://github.com/cddmp/enum4linux-ng)
[Original Enum4Linux](https://github.com/CiscoCXSecurity/enum4linux)

# Installing
## Kali
```
sudo apt install enum4linux-ng
```
## Debian based
- Install Pre Reqs
```
sudo apt install -y smbclient python3-ldap3 python3-yaml python3-impacket
```
- Best done in an a VENV
```
git clone https://github.com/cddmp/enum4linux-ng && cd enum4linux-ng
pip install wheel
pip install -r requirements.txt
```
# Usage
- Basic usage
```
python3 enum4linux-ng.py -As <target>
```