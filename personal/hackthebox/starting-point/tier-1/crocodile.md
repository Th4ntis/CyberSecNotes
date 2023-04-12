# Crocodile

## Initial Scan

```bash
nmap -sV -sT -sC -T4 -v 10.129.208.251
Starting Nmap 7.80 ( https://nmap.org ) at 2022-08-23 20:31 EDT
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 20:31
Completed NSE at 20:31, 0.00s elapsed
Initiating NSE at 20:31
Completed NSE at 20:31, 0.00s elapsed
Initiating NSE at 20:31
Completed NSE at 20:31, 0.00s elapsed
Initiating Ping Scan at 20:31
Scanning 10.129.208.251 [2 ports]
Completed Ping Scan at 20:31, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 20:31
Completed Parallel DNS resolution of 1 host. at 20:31, 0.08s elapsed
Initiating Connect Scan at 20:31
Scanning 10.129.208.251 [1000 ports]
Discovered open port 80/tcp on 10.129.208.251
Discovered open port 21/tcp on 10.129.208.251
Completed Connect Scan at 20:31, 0.69s elapsed (1000 total ports)
Initiating Service scan at 20:31
Scanning 2 services on 10.129.208.251
Completed Service scan at 20:31, 6.09s elapsed (2 services on 1 host)
NSE: Script scanning 10.129.208.251.
Initiating NSE at 20:31
NSE: [ftp-bounce] PORT response: 500 Illegal PORT command.
Completed NSE at 20:31, 1.03s elapsed
Initiating NSE at 20:31
Completed NSE at 20:31, 0.18s elapsed
Initiating NSE at 20:31
Completed NSE at 20:31, 0.00s elapsed
Nmap scan report for 10.129.208.251
Host is up (0.047s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 ftp      ftp            33 Jun 08  2021 allowed.userlist
|_-rw-r--r--    1 ftp      ftp            62 Apr 20  2021 allowed.userlist.passwd
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.9
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-favicon: Unknown favicon MD5: 1248E68909EAE600881B8DB1AD07F356
| http-methods: 
|_  Supported Methods: OPTIONS HEAD GET POST
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Smash - Bootstrap Business Template
Service Info: OS: Unix

NSE: Script Post-scanning.
Initiating NSE at 20:31
Completed NSE at 20:31, 0.00s elapsed
Initiating NSE at 20:31
Completed NSE at 20:31, 0.00s elapsed
Initiating NSE at 20:31
Completed NSE at 20:31, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.53 seconds
```

## Task 1

#### What nmap scanning switch employs the use of default scripts during a scan?

Found from `nmap --help`

```bash
nmap --help | grep script
  -sC: equivalent to --script=default
```

Answer: -sC

## Task 2

#### What service version is found to be running on port 21?

Found in initial scan.

Answer: vsFTPd 3.0.3

## Task 3

#### What FTP code is returned to us for the "Anonymous FTP login allowed" message?

Google - I don't have all status codes memorized.

Answer: 230

## Task 4

#### What command can we use to download the files we find on the FTP server?

Previous knowledge of using FTP before.&#x20;

Answer: get

## Task 5

#### What is one of the higher-privilege sounding usernames in the list we retrieved?

A default typical high privilege account.

Answer: admin

## Task 6

#### What version of Apache HTTP Server is running on the target host?

Found in the initial scan.

Answer: 2.4.41

## Task 7

#### What is the name of a handy web site analysis plug-in we can install in our browser?

Known from previous knowledge, google "web site analysis plug-in" helps find this answer as well.

Answer: Wappalyzer

## Task 8

#### What switch can we use with gobuster to specify we are looking for specific filetypes?

Found from running `gobuster --help`.&#x20;

Answer: -x

## Task 9

#### What file have we found that can provide us a foothold on the target?

Running gobuster against the host:

```bash
gobuster -x php -w /opt/SecLists/Discovery/Web-Content/Common-PHP-Filenames.txt -u (IP)
```

```bash
=====================================================
Gobuster v2.0.1              OJ Reeves (@TheColonial)
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://10.129.208.251/
[+] Threads      : 10
[+] Wordlist     : /opt/SecLists/Discovery/Web-Content/Common-PHP-Filenames.txt
[+] Status codes : 200,204,301,302,307,403
[+] Extensions   : php
[+] Timeout      : 10s
=====================================================
2022/08/23 20:47:39 Starting gobuster
=====================================================
/config.php (Status: 200)
/login.php (Status: 200)
/logout.php (Status: 302)
=====================================================
2022/08/23 20:48:35 Finished
=====================================================
```

Answer: login.php

## Task 10

#### Submit root flag

If we first FTP into the machine with an anonymous account

```bash
ftp 10.129.208.251
Connected to 10.129.208.251.
220 (vsFTPd 3.0.3)
Name (10.129.208.251:th4ntis): anonymous
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 
```

We can see a list of a file and `get` them to our machine

```bash
ftp> ls
229 Entering Extended Passive Mode (|||47529|)
150 Here comes the directory listing.
-rw-r--r--    1 ftp      ftp            33 Jun 08  2021 allowed.userlist
-rw-r--r--    1 ftp      ftp            62 Apr 20  2021 allowed.userlist.passwd
226 Directory send OK.
ftp> get allowed.userlist
local: allowed.userlist remote: allowed.userlist
229 Entering Extended Passive Mode (|||47804|)
150 Opening BINARY mode data connection for allowed.userlist (33 bytes).
100% |****************************************************************************|    33       14.91 KiB/s    00:00 ETA
226 Transfer complete.
33 bytes received in 00:00 (0.69 KiB/s)
ftp> get allowed.userlist.passwd
local: allowed.userlist.passwd remote: allowed.userlist.passwd
229 Entering Extended Passive Mode (|||49809|)
150 Opening BINARY mode data connection for allowed.userlist.passwd (62 bytes).
100% |****************************************************************************|    62        3.11 MiB/s    00:00 ETA
226 Transfer complete.
62 bytes received in 00:00 (1.37 KiB/s)
ftp>
```

now lets cat the files and just work with what it's there

```bash
cat allowed.userlist
aron
pwnmeow
egotisticalsw
admin
╭─    ~                                                                                                          ✔ 
╰─ cat allowed.userlist.passwd 
root
Supersecretpassword1
@BaASD&9032123sADS
rKXM59ESxesUFHAdbas
```

After attempting: admin:rKXM59ESxesUFHAd we were able to log in and get our flag.

<figure><img src="../../../../.gitbook/assets/image (7) (1) (3).png" alt=""><figcaption></figcaption></figure>

Answer:  c7110277ac44d78b6a9fff2232434d16
