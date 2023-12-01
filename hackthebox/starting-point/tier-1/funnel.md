# Funnel

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.246.65 -oA Funnel
```

<figure><img src="../../../.gitbook/assets/image (11) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Task 1

How many TCP ports are open?

Answer: 2

## Task 2

What is the name of the directory that is available on the FTP server?

<figure><img src="../../../.gitbook/assets/image (12) (1) (1).png" alt=""><figcaption></figcaption></figure>

Answer: mail\_backup

## Task 3

What is the default account password that every new member on the "Funnel" team should change as soon as possible? - Look in the .pdf file from the FTP server.

<figure><img src="../../../.gitbook/assets/image (13) (1) (1).png" alt=""><figcaption></figcaption></figure>

Answer: funnel123#!#

## Task 4

Which user has not changed their default password yet?

<figure><img src="../../../.gitbook/assets/image (14) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure>

Answer: christine

## Task 5

Which service is running on TCP port 5432 and listens only on localhost?

<figure><img src="../../../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>

Answer: postgresql

## Task 6

Since you can't access the previously mentioned service from the local machine, you will have to create a tunnel and connect to it from your machine. What is the correct type of tunneling to use? remote port forwarding or local port forwarding?

Answer: local port tunneling

## Task 7

What is the name of the database that holds the flag?

<figure><img src="../../../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

Answer: Secrets

## Task 8

Could you use a dynamic tunnel instead of local port forwarding? Yes or No.

Answer: Yes

## Task 9

Submit Root Flag

<figure><img src="../../../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

Answer: cf277664b1771217d7006acdea006db1
