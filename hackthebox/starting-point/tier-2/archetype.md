# Archetype

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.95.187 -oA Archetype
```

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

## Task 1

Which TCP port is hosting a database server?

Answer: 1433

## Task 2

What is the name of the non-Administrative share available over SMB?

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Answer: backups

## Task 3

What is the password identified in the file on the SMB share?

<figure><img src="../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Answer: M3g4c0rp123

## Task 4

What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server?

<figure><img src="../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Answer: mssqlclient.py

## Task 5

What extended stored procedure of Microsoft SQL Server can be used in order to spawn a Windows command shell?

<figure><img src="../../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Answer:xp\_cmdshell

## Task 6

What script can be used in order to search possible paths to escalate privileges on Windows hosts? [PEASS Github](https://github.com/carlospolop/PEASS-ng) Answer: winpeas

## Task 7

What file contains the administrator's password?

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

Answer: ConsoleHost\_History.txt

## Task 8

Submit user flag

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Answer: 3e7b102e78218e935bf3f4951fec21a3

## Task 9

Submit root flag&#x20;

<figure><img src="../../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

```powershell
.\winPEASx64.exe
```

<figure><img src="../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

Administrator Password: `MEGACORP_4dm1n!!`

<figure><img src="../../../.gitbook/assets/image (512).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (513).png" alt=""><figcaption></figcaption></figure>

Answer: b91ccec3305e98240082d4474b848528
