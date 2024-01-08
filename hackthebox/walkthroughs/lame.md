# Lame

## Initial Scan

```nmap
sudo nmap -T4 -v 10.129.111.164 -oA Lame
sudo nmap -T4 -p 21,22,139,445 -sV -v 10.129.111.164 -oA Lame
```

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

## FTP

Anonymous Login is enabled

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

## SMB

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

&#x20;Only have access to tmp

&#x20;&#x20;

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

## MSFconsole

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

So it's not Vuln to MS17-010(EternalBlue). Check for SMB Version Vulnerabilities

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

[Rapid7 Document](https://www.rapid7.com/db/modules/exploit/multi/samba/usermap\_script/)

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (949).png" alt=""><figcaption></figcaption></figure>

User Flag: a6a83ea02ff14ca4aa497dad8c2f775

<figure><img src="../../.gitbook/assets/image (950).png" alt=""><figcaption></figcaption></figure>

Root Flag: 162680cf1f47cde0affaecd104a59588

&#x20;

<figure><img src="../../.gitbook/assets/image (951).png" alt=""><figcaption></figcaption></figure>
