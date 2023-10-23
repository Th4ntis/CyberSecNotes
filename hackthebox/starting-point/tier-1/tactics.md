# Tactics

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.123.121 -oA Tactics
```

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

## Task 1

Which Nmap switch can we use to enumerate machines when our ping ICMP packets are blocked by the Windows firewall?

<figure><img src="../../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

Answer: -Pn

## Task 2

What does the 3-letter acronym SMB stand for?

Answer: Server Message Block

## Task 3

What port does SMB use to operate at?

Answer: 445

## Task 4

What command line argument do you give to `smbclient` to list available shares?

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Answer: -L

## Task 5

What character at the end of a share name indicates it's an administrative share?

Answer: $

## Task 6

Which Administrative share is accessible on the box that allows users to view the whole file system?

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

Answer: C$

## Task 7

What command can we use to download the files we find on the SMB Share?

Answer: get

## Task 8

Which tool that is part of the Impacket collection can be used to get an interactive shell on the system?

Answer: psexec.py

## Task 9

Submit root flag

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Answer: f751c19eda8f61ce81827e6930a1f40c
