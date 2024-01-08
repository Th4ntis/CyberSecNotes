# Archetype

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.95.187 -oA Archetype
```

<figure><img src="../../../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

## Task 1

Which TCP port is hosting a database server?

Answer: 1433

## Task 2

What is the name of the non-Administrative share available over SMB?

<figure><img src="../../../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Answer: backups

## Task 3

What is the password identified in the file on the SMB share?

<figure><img src="../../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>

Answer: M3g4c0rp123

## Task 4

What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server?

<figure><img src="../../../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

Answer: mssqlclient.py

## Task 5

What extended stored procedure of Microsoft SQL Server can be used in order to spawn a Windows command shell?

<figure><img src="../../../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

Answer:xp\_cmdshell

## Task 6

What script can be used in order to search possible paths to escalate privileges on Windows hosts? [PEASS Github](https://github.com/carlospolop/PEASS-ng) Answer: winpeas

## Task 7

What file contains the administrator's password?

<figure><img src="../../../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

Answer: ConsoleHost\_History.txt

## Task 8

Submit user flag

<figure><img src="../../../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

Answer: 3e7b102e78218e935bf3f4951fec21a3

## Task 9

Submit root flag&#x20;

<figure><img src="../../../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

```powershell
.\winPEASx64.exe
```

<figure><img src="../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

Administrator Password: `MEGACORP_4dm1n!!`

<figure><img src="../../../.gitbook/assets/image (868).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (869).png" alt=""><figcaption></figcaption></figure>

Answer: b91ccec3305e98240082d4474b848528
