# Lame

## Initial Scan

```nmap
sudo nmap -T4 -v 10.129.111.164 -oA Lame
sudo nmap -T4 -p 21,22,139,445 -sV -v 10.129.111.164 -oA Lame
```

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## FTP

Anonymous Login is enabled

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

## SMB

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;Only have access to tmp

&#x20;&#x20;

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

## MSFconsole

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

So it's not Vuln to MS17-010(EternalBlue). Check for SMB Version Vulnerabilities

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

[Rapid7 Document](https://www.rapid7.com/db/modules/exploit/multi/samba/usermap\_script/)

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (593).png" alt=""><figcaption></figcaption></figure>

User Flag: a6a83ea02ff14ca4aa497dad8c2f775

<figure><img src="../../.gitbook/assets/image (594).png" alt=""><figcaption></figcaption></figure>

Root Flag: 162680cf1f47cde0affaecd104a59588

&#x20;

<figure><img src="../../.gitbook/assets/image (595).png" alt=""><figcaption></figcaption></figure>
