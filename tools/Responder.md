# About
Responder is a LLMNR, NBT-NS and MDNS poisoner, with built-in HTTP/SMB/MSSQL/FTP/LDAP rogue authentication server supporting NTLMv1/NTLMv2/LMv2, Extended Security NTLMSSP and Basic HTTP authentication.
## Links
[Github](https://github.com/lgandx/Responder)
# Installing
- Source - Preferable in a VENV
```
git clone https://github.com/lgandx/Responder.git && cd Responder
python3 -m pip install netifaces
sudo python3 Responder.py
```
# Usage
- Responder.conf file location:
```
/etc/responder/Responder.conf
```
Typically turn off SMB and HTTP if capturing relays with NTLMYRelayX

- Default with HTTP and SMB on
```
sudo python3 /usr/share/responder/Responder.py -I eth
```

- Responder logs location:
```
/usr/share/responder/logs
```

- Responder.py location:
```
/usr/share/responder/Responder.py
```

- Analyze mode
```
Responder -I eth0 -A
```

- Proxy, DHCP, verbose, downgrade
```
sudo python3 /usr/share/responder/Responder.py -I eth0 -PDv --lm
```