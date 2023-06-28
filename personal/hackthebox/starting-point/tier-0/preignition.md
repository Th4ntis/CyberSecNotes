# Preignition

## Initial Scan

```bash
sudo nmap -p- -sT -sV -T4 -v 10.129.16.210
Starting Nmap 7.80 ( https://nmap.org ) at 2022-08-07 21:16 EDT
NSE: Loaded 45 scripts for scanning.
Initiating Ping Scan at 21:16
Scanning 10.129.16.210 [4 ports]
Completed Ping Scan at 21:16, 0.08s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 21:16
Completed Parallel DNS resolution of 1 host. at 21:16, 0.10s elapsed
Initiating Connect Scan at 21:16
Scanning 10.129.16.210 [65535 ports]
Discovered open port 80/tcp on 10.129.16.210
Completed Connect Scan at 21:17, 51.35s elapsed (65535 total ports)
Initiating Service scan at 21:17
Scanning 1 service on 10.129.16.210
Completed Service scan at 21:17, 6.11s elapsed (1 service on 1 host)
NSE: Script scanning 10.129.16.210.
Initiating NSE at 21:17
Completed NSE at 21:17, 0.27s elapsed
Initiating NSE at 21:17
Completed NSE at 21:17, 0.23s elapsed
Nmap scan report for 10.129.16.210
Host is up (0.055s latency).
Not shown: 65534 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    nginx 1.14.2

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 58.48 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (40B)

```

## Task 1

#### What is considered to be one of the most essential skills to possess as a Penetration Tester?

Answer: Dir busting

## Task 2

#### What switch do we use for nmap's scan to specify that we want to perform version detection

nmap --help

Answer: -sV

## Task 3

#### What does Nmap report is the service identified as running on port 80/tcp?

Found in initial scan

Answer: http

## Task 4

#### What server name and version of service is running on port 80/tcp?

Found in initial scan

Answer: nginx 1.14.2

## Task 5

#### What switch do we use to specify to Gobuster we want to perform dir busting specifically?

[Gobuster man page](https://manpages.ubuntu.com/manpages/impish/man1/gobuster.1.html)

![](<../../../../.gitbook/assets/image (5) (1) (1).png>)

Answer: dir

## Task 6

#### What page is found during our dir busting activities?

![](<../../../../.gitbook/assets/image (1) (2) (3).png>)

Answer: admin.php

## Task 7

#### What is the HTTP status code reported by Gobuster for the discovered page?

Previous screenshot

Answer: 200

## Task 8

#### Submit root flag

When browsing to (IP)/admin.php

![](<../../../../.gitbook/assets/image (3) (1) (1) (3).png>)

Took a stab in the dark with **admin:admin**

![](<../../../../.gitbook/assets/image (8) (3).png>)

Answer: **6483bee07c1c1d57f14e5b0717503c73**
