# Base

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.246.67 -oA Base
```

<figure><img src="../../../.gitbook/assets/image (989).png" alt=""><figcaption></figcaption></figure>

## Task 1

Which two TCP ports are open on the remote host?

Answer: 22,80

## Task 2

What is the relative path on the webserver for the login page?

<figure><img src="../../../.gitbook/assets/image (990).png" alt=""><figcaption></figcaption></figure>

Answer: /login/login.php

## Task 3

How many files are present in the '/login' directory?

<figure><img src="../../../.gitbook/assets/image (991).png" alt=""><figcaption></figcaption></figure>

Answer: 3

## Task 4

What is the file extension of a swap file?

<figure><img src="../../../.gitbook/assets/image (992).png" alt=""><figcaption></figcaption></figure>

Answer: .swp

## Task 5

Which PHP function is being used in the backend code to compare the user submitted username and password to the valid username and password?

<figure><img src="../../../.gitbook/assets/image (993).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (994).png" alt=""><figcaption></figcaption></figure>

Answer: `strcmp()`

## Task 6

In which directory are the uploaded files stored?

<figure><img src="../../../.gitbook/assets/image (995).png" alt=""><figcaption></figcaption></figure>

Modify the request to

<figure><img src="../../../.gitbook/assets/image (996).png" alt=""><figcaption></figcaption></figure>

Send it and open it in the browser

<figure><img src="../../../.gitbook/assets/image (997).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (998).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (999).png" alt=""><figcaption></figcaption></figure>

Answer: \_uploaded

## Task 7

Which user exists on the remote host with a home directory?

Upload a webshell

<figure><img src="../../../.gitbook/assets/image (1000).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1001).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1002).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1003).png" alt=""><figcaption></figcaption></figure>

Encode the command

<figure><img src="../../../.gitbook/assets/image (1004).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1005).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (1006).png" alt=""><figcaption></figcaption></figure>

Answer: john

## Task 8

What is the password for the user present on the system?

Looking at the "empty" config.php file

<figure><img src="../../../.gitbook/assets/image (1007).png" alt=""><figcaption></figcaption></figure>

Answer: thisisagoodpassword

## Task 9

What is the full path to the command that the user john can run as user root on the remote host?

Login as John with the new password we found

<figure><img src="../../../.gitbook/assets/image (1008).png" alt=""><figcaption></figcaption></figure>

Answer: /usr/bin/find

## Task 10

What action can the find command use to execute commands?

Looking on [GTFOBins](https://gtfobins.github.io/gtfobins/find/) we can see

<figure><img src="../../../.gitbook/assets/image (1009).png" alt=""><figcaption></figcaption></figure>

```bash
sudo find . -exec /bin/sh \; -quit
```

Answer: exec

## Task 11

User Flag

<figure><img src="../../../.gitbook/assets/image (1010).png" alt=""><figcaption></figcaption></figure>

Answer:f54846c258f3b4612f78a819573d158e

## Task 12

Root Flag

<figure><img src="../../../.gitbook/assets/image (1011).png" alt=""><figcaption></figcaption></figure>

Answer: 51709519ea18ab37dd6fc58096bea949
