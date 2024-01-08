# Ignition

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.1.27 -oA Ignition
```

<figure><img src="../../../.gitbook/assets/image (858).png" alt=""><figcaption></figcaption></figure>

## Task 1

Which service version is found to be running on port 80? - Found within the initial scan

Answer: nginx 1.14.2

## Task 2

What is the 3-digit HTTP status code returned when you visit http://10.129.1.27/? - When going to the website, we get an error but doesn't tell us an error code.

<figure><img src="../../../.gitbook/assets/image (859).png" alt=""><figcaption></figcaption></figure>

If we curl the site instead, we get the error code.

```bash
curl -v http://10.129.1.27/
```

<figure><img src="../../../.gitbook/assets/image (860).png" alt=""><figcaption></figcaption></figure>

Answer: 302

## Task 3

What is the virtual host name the webpage expects to be accessed by? - This is found in the URL when attempting to go to the website via it's IP instead of the hostname.

<figure><img src="../../../.gitbook/assets/image (861).png" alt=""><figcaption></figcaption></figure>

Answer: ignition.htb

## Task 4

What is the full path to the file on a Linux computer that holds a local list of domain name to IP address pairs?

Answer: /etc/hosts

## Task 5

Use a tool to brute force directories on the webserver. What is the full URL to the Magento login page?

Add the IP and domain to our hosts file

<figure><img src="../../../.gitbook/assets/image (862).png" alt=""><figcaption></figcaption></figure>

Use Gobuster to do some directory traversal

```bash
gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -u http://ignition.htb
```

<figure><img src="../../../.gitbook/assets/image (863).png" alt=""><figcaption></figcaption></figure>

Answer: http://ignition.htb/admin

## Task 6

Look up the password requirements for Magento and also try searching for the most common passwords of 2023. Which password provides access to the admin account?

After looking into Magento default credentials and none of the defaults(admin:admin etc) worked, I loaded up BurpSuite, used the Burp Browser, attempted to login with creds, put the POST request into Intruder and performed a BruteForce attack with various default passwords.

<figure><img src="../../../.gitbook/assets/image (864).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (865).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (866).png" alt=""><figcaption></figcaption></figure>

Answer: qwerty123

## Task 7

Submit root flag

<figure><img src="../../../.gitbook/assets/image (867).png" alt=""><figcaption></figcaption></figure>

Answer: 797d6c988d9dc5865e010b9410f247e0
