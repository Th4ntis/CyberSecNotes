# Explosion

## Initial Scan

```bash
sudo nmap -p- -sT -sV -T4 -v 10.129.16.206
[sudo] password for th4ntis: 
Starting Nmap 7.80 ( https://nmap.org ) at 2022-08-07 21:02 EDT
NSE: Loaded 45 scripts for scanning.
Initiating Ping Scan at 21:02
Scanning 10.129.16.206 [4 ports]
Completed Ping Scan at 21:02, 0.07s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 21:02
Completed Parallel DNS resolution of 1 host. at 21:02, 0.09s elapsed
Initiating Connect Scan at 21:02
Scanning 10.129.16.206 [65535 ports]
Discovered open port 139/tcp on 10.129.16.206
Discovered open port 445/tcp on 10.129.16.206
Discovered open port 3389/tcp on 10.129.16.206
Discovered open port 135/tcp on 10.129.16.206
Discovered open port 47001/tcp on 10.129.16.206
Discovered open port 49667/tcp on 10.129.16.206
Discovered open port 5985/tcp on 10.129.16.206
Discovered open port 49669/tcp on 10.129.16.206
Discovered open port 49665/tcp on 10.129.16.206
Discovered open port 49668/tcp on 10.129.16.206
Connect Scan Timing: About 44.68% done; ETC: 21:03 (0:00:38 remaining)
Discovered open port 49664/tcp on 10.129.16.206
Discovered open port 49671/tcp on 10.129.16.206
Discovered open port 49666/tcp on 10.129.16.206
Discovered open port 49670/tcp on 10.129.16.206
Completed Connect Scan at 21:03, 60.76s elapsed (65535 total ports)
Initiating Service scan at 21:03
Scanning 14 services on 10.129.16.206
Service scan Timing: About 50.00% done; ETC: 21:05 (0:00:55 remaining)
Completed Service scan at 21:04, 57.52s elapsed (14 services on 1 host)
NSE: Script scanning 10.129.16.206.
Initiating NSE at 21:04
Completed NSE at 21:04, 0.36s elapsed
Initiating NSE at 21:04
Completed NSE at 21:04, 0.25s elapsed
Nmap scan report for 10.129.16.206
Host is up (0.058s latency).
Not shown: 65521 closed ports
PORT      STATE SERVICE       VERSION
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

## Task 1

#### What does the 3-letter acronym RDP stand for?

Answer: Remote Desktop Protocol

## Task 2

#### What is a 3-letter acronym that refers to interaction with the host through a command line interface?

Answer: CLI

## Task 3

#### What about graphical user interface interactions?

Answer:  GUI

## Task 4

#### What is the name of an old remote access tool that came without encryption by default and listens on TCP port 23?

Answer: Telnet

## Task 5

#### What is the name of the service running on port 3389 TCP?

Found from initial scan

Answer: ms-wbt-server

## Task 6

#### What is the switch used to specify the target host's IP address when using xfreerdp?

[xfreerdp man page](https://www.mankier.com/1/xfreerdp)

Answer: /v:

## Task 7

#### Submit root flag

![](<../../../../.gitbook/assets/image (6).png>)

Answer: 951fa96d7830c451b536be5a6be008a0
