# Enumeration

## Web directory

```bash
gobuster dir --url http://(ip) -w (wordlist)
```

```bash
ffuf -recursion -mc all -ac -c -e (X) -w (wordlist) 
```

```bash
ffuf -recursion -mc all -ac -c -e .htm,.shtml,.php,.html,.js,.txt,.zip,.bak,.asp,.aspx,.xml -w /usr/share/seclists/Discovery/Web-Content/big.txt -u https://domain.com/FUZZ -fc 400,401,403,404,406,500,502 > file.txt
```

```bash
nikto -h http://ip
```

## SMB

List directories

```bash
smbclient -L (ip)
```
