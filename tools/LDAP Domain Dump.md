# About
Active Directory information dumper via LDAP. In an Active Directory domain, a lot of interesting information can be retrieved via LDAP by any authenticated user (or machine). This makes LDAP an interesting protocol for gathering information in the recon phase of a pentest of an internal network. A problem is that data from LDAP often is not available in an easy to read format.

ldapdomaindump is a tool which aims to solve this problem, by collecting and parsing information available via LDAP and outputting it in a human readable HTML format, as well as machine readable json and csv/tsv/greppable files.
## Links
[Github](https://github.com/dirkjanm/ldapdomaindump)
# Installing
- Source
```
git clone https://github.com/dirkjanm/ldapdomaindump.git && cd ldapdomaindump
python setup.py
```

- pip
```
pip install ldapdomaindump
```
# Usage
```
sudo ldapdomaindump -u DOMAIN\\USER -p PASSWORD IP
```