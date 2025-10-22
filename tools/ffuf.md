# FFUF

## About

Fuzz Faster U Fool. A fast web fuzzer written in Go

### Links

[Github](https://github.com/ffuf/ffuf)

[Daniel Miessler primer on ffuf](https://danielmiessler.com/p/ffuf/)

## Installing

* Download prebuilt binary from https://github.com/ffuf/ffuf/releases/latest
* If GO Compiler is installed

```
go install github.com/ffuf/ffuf/v2@latest
```

* From source

```
git clone https://github.com/ffuf/ffuf ; cd ffuf ; go get ; go build
```

## Usage

```
ffuf -recursion -mc all -ac -c -e (X) -w WORDLIST
```

```
ffuf -recursion -mc all -ac -c -e .htm,.shtml,.php,.html,.js,.txt,.zip,.bak,.asp,.aspx,.xml -w WORDLIST -u https://TARGET/FUZZ -fc 400,401,403,404,406,500,502 > OutFile.txt
```

```
ffuf -recursion -mc all -ac -c -e .htm,.shtml,.php,.html,.js,.txt,.zip,.bak,.asp,.aspx,.xml -w WORDLIST -u https://TARGET/FUZZ -fc 400,403,404,500 > OutFile.txt
```

```bash
ffuf -recursion -mc all -ac -c -e (X) -w (wordlist)
```

```bash
ffuf -recursion -mc all -ac -c -e .htm,.shtml,.php,.html,.js,.txt,.zip,.bak,.asp,.aspx,.xml -w /usr/share/seclists/Discovery/Web-Content/big.txt -u <https://domain.com/FUZZ> -fc 400,401,403,404,406,500,502 > file.txt
```

* Password Guessing with POST request

```bash
ffuf -request ire-request.txt -request-proto http -mode clusterbomb -w Users.txt:FUZZUSER -w Wordlists/combined.txt:FUZZPASS -fc 301
```

```bash
ffuf -request teashop.txt -request-proto http -mode clusterbomb -w pw.txt:FUZZPASS -w /usr/share/seclists/Usernames/top-usernames-shortlist.txt:FUZZUSERS -fs 3376
```
