# Unified

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.96.149 -oA Unified
```

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.96.149 -oA Unified
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-26 04:39 EDT
<snip>
Discovered open port 8080/tcp on 10.129.96.149
Discovered open port 22/tcp on 10.129.96.149
Discovered open port 8443/tcp on 10.129.96.149
Discovered open port 6789/tcp on 10.129.96.149
Completed SYN Stealth Scan at 04:39, 1.56s elapsed (1000 total ports)
Initiating Service scan at 04:39
Scanning 4 services on 10.129.96.149
Completed Service scan at 04:42, 156.77s elapsed (4 services on 1 host)
NSE: Script scanning 10.129.96.149.
Initiating NSE at 04:42
Completed NSE at 04:42, 14.31s elapsed
Initiating NSE at 04:42
Completed NSE at 04:42, 1.08s elapsed
Initiating NSE at 04:42
Completed NSE at 04:42, 0.00s elapsed
Nmap scan report for 10.129.96.149
Host is up (0.020s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE         VERSION
22/tcp   open  ssh             OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48:ad:d5:b8:3a:9f:bc:be:f7:e8:20:1e:f6:bf:de:ae (RSA)
|   256 b7:89:6c:0b:20:ed:49:b2:c1:86:7c:29:92:74:1c:1f (ECDSA)
|_  256 18:cd:9d:08:a6:21:a8:b8:b6:f7:9f:8d:40:51:54:fb (ED25519)
6789/tcp open  ibm-db2-admin?
8080/tcp open  http-proxy
|_http-title: Did not follow redirect to https://10.129.96.149:8443/manage
|_http-open-proxy: Proxy might be redirecting requests
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.1 404 
|     Content-Type: text/html;charset=utf-8
|     Content-Language: en
|     Content-Length: 431
|     Date: Thu, 26 Oct 2023 08:39:50 GMT
|     Connection: close
|     <!doctype html><html lang="en"><head><title>HTTP Status 404 
|     Found</title><style type="text/css">body {font-family:Tahoma,Arial,sans-serif;} h1, h2, h3, b {color:white;background-color:#525D76;} h1 {font-size:22px;} h2 {font-size:16px;} h3 {font-size:14px;} p {font-size:12px;} a {color:black;} .line {height:1px;background-color:#525D76;border:none;}</style></head><body><h1>HTTP Status 404 
|     Found</h1></body></html>
|   GetRequest, HTTPOptions: 
|     HTTP/1.1 302 
|     Location: http://localhost:8080/manage
|     Content-Length: 0
|     Date: Thu, 26 Oct 2023 08:39:50 GMT
|     Connection: close
|   RTSPRequest, Socks5: 
|     HTTP/1.1 400 
|     Content-Type: text/html;charset=utf-8
|     Content-Language: en
|     Content-Length: 435
|     Date: Thu, 26 Oct 2023 08:39:50 GMT
|     Connection: close
|     <!doctype html><html lang="en"><head><title>HTTP Status 400 
|     Request</title><style type="text/css">body {font-family:Tahoma,Arial,sans-serif;} h1, h2, h3, b {color:white;background-color:#525D76;} h1 {font-size:22px;} h2 {font-size:16px;} h3 {font-size:14px;} p {font-size:12px;} a {color:black;} .line {height:1px;background-color:#525D76;border:none;}</style></head><body><h1>HTTP Status 400 
|_    Request</h1></body></html>
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
8443/tcp open  ssl/nagios-nsca Nagios NSCA
| http-title: UniFi Network
|_Requested resource was /manage/account/login?redirect=%2Fmanage
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| ssl-cert: Subject: commonName=UniFi/organizationName=Ubiquiti Inc./stateOrProvinceName=New York/countryName=US
| Subject Alternative Name: DNS:UniFi
| Issuer: commonName=UniFi/organizationName=Ubiquiti Inc./stateOrProvinceName=New York/countryName=US
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2021-12-30T21:37:24
| Not valid after:  2024-04-03T21:37:24
| MD5:   e6be:8c03:5e12:6827:d1fe:612d:dc76:a919
|_SHA-1: 111b:aa11:9cca:4401:7cec:6e03:dc45:5cfe:65f6:d829
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
<snip>
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

## Task 1

Which are the first four open ports?

Answer: 22,6789,8080,8443

## Task 2

What is the title of the software that is running running on port 8443?

Answer: UniFi Network

## Task 3

What is the version of the software that is running?

<figure><img src="../../../.gitbook/assets/image (579).png" alt=""><figcaption></figcaption></figure>

Answer: 6.4.54

## Task 4

What is the CVE for the identified vulnerability?

<figure><img src="../../../.gitbook/assets/image (580).png" alt=""><figcaption></figcaption></figure>

Answer: CVE-2021-44228

## Task 5

What protocol does JNDI leverage in the injection?

<figure><img src="../../../.gitbook/assets/image (581).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (582).png" alt=""><figcaption></figcaption></figure>

Answer: ldap

## Task 6

What tool do we use to intercept the traffic, indicating the attack was successful?

Answer: tcpdump

## Task 7

What port do we need to inspect intercepted traffic for?

Answer: 389

## Task 8

What port is the MongoDB service running on?

<figure><img src="../../../.gitbook/assets/image (583).png" alt=""><figcaption></figcaption></figure>

Answer: 27117

## Task 9

What is the default database name for UniFi applications?

<figure><img src="../../../.gitbook/assets/image (584).png" alt=""><figcaption></figcaption></figure>

Answer: ace

## Task 10

What is the function we use to enumerate users within the database in MongoDB?

Answer: db.admin.find()

## Task 11

What is the function we use to update users within the database in MongoDB?

Answer: db.admin.update()

## Task 12

What is the password for the root user? Grab admin PW from MongoDB

```bash
mongo --port 27117 ace --eval "db.admin.find().forEach(printjson);"
```

<figure><img src="../../../.gitbook/assets/image (585).png" alt=""><figcaption></figcaption></figure>

Update admin password

```bash
mkpasswd -m sha-512 Password1234

$6$sbnjIZBtmRds.L/E$fEKZhosqeHykiVWT1IBGju43WdVdDauv5RsvIPifi32CC2TTNU8kHOd2ToaW8fIX7XXM8P5Z8j4NB1gJGTONl1
```

```bash
mongo --port 27117 ace --eval 'db.admin.update({"_id": ObjectId("61ce278f46e0fb0012d47ee4")},{$set:{"x_shadow":"$6$ttw6pQsuECHKIDhO$zNY4cTuEmzd8kpQZHShWAIms1LpeEyH7NfcYXVpK3FN6mzwgKyf21T2208HS0jt4Ve.wSpifTfKbN4pcpqiL8/"}})'
```

<figure><img src="../../../.gitbook/assets/image (586).png" alt=""><figcaption></figcaption></figure>

Login with `administrator:Password1234`

<figure><img src="../../../.gitbook/assets/image (587).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (588).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (589).png" alt=""><figcaption></figcaption></figure>

Answer: NotACrackablePassword4U2022

## Task 13

Submit User Flag

<figure><img src="../../../.gitbook/assets/image (590).png" alt=""><figcaption></figcaption></figure>

Answer: 6ced1a6a89e666c0620cdb10262ba127

## Task 14

Submit Root Flag

<figure><img src="../../../.gitbook/assets/image (591).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (592).png" alt=""><figcaption></figcaption></figure>

Answer: e50bc93c75b634e4b272d2f771c33681
