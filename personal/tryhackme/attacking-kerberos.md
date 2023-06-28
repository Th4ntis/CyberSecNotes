---
description: 'This is my notes for the TryHackMe Room: Attacking Kerberos.'
---

# Attacking Kerberos

This room can be found [here](https://tryhackme.com/room/attackingkerberos). This room is pretty straight forward in explaining what it wants us to do so there's not much of a walkthrough needed for this. This room is more to help us understand what Kerberos is and methods to attack it. I have some notes on Kerberos and Kerberoasting [here](../../general/attack-and-defense/methods/kerberos-and-kerberoasting.md).

## Task 1

### What is Kerberos?

Kerberos is the default authentication service for Microsoft Windows domains. It is intended to be more "secure" than NTLM by using third party ticket authorization as well as stronger encryption. Even though NTLM has a lot more attack vectors to choose from Kerberos still has a handful of underlying vulnerabilities just like NTLM that we can use to our advantage.

Common Terminology

* **Ticket Granting Ticket (TGT)** - A ticket-granting ticket is an authentication ticket used to request service tickets from the TGS for specific resources from the domain.
* **Key Distribution Center (KDC)** - The Key Distribution Center is a service for issuing TGTs and service tickets that consist of the Authentication Service and the Ticket Granting Service.
* **Authentication Service (AS)** - The Authentication Service issues TGTs to be used by the TGS in the domain to request access to other machines and service tickets.
* **Ticket Granting Service (TGS)** - The Ticket Granting Service takes the TGT and returns a ticket to a machine on the domain.
* **Service Principal Name (SPN)** - A Service Principal Name is an identifier given to a service instance to associate a service instance with a domain service account. Windows requires that services have a domain service account which is why a service needs an SPN set.
* **KDC Long Term Secret Key (KDC LT Key)** - The KDC key is based on the KRBTGT service account. It is used to encrypt the TGT and sign the PAC.
* **Client Long Term Secret Key (Client LT Key)** - The client key is based on the computer or service account. It is used to check the encrypted timestamp and encrypt the session key.
* **Service Long Term Secret Key (Service LT Key)** - The service key is based on the service account. It is used to encrypt the service portion of the service ticket and sign the PAC.
* **Session Key** - Issued by the KDC when a TGT is issued. The user will provide the session key to the KDC along with the TGT when requesting a service ticket.
* **Privilege Attribute Certificate (PAC)** - The PAC holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the Target LT Key and the KDC LT Key in order to validate the user.

![Kerberos Authentication](<../../.gitbook/assets/image (157).png>)

1. The client requests an Authentication Ticket or Ticket Granting Ticket (TGT).
2. The Key Distribution Center verifies the client and sends back an encrypted TGT.
3. The client sends the encrypted TGT to the Ticket Granting Server (TGS) with the Service Principal Name (SPN) of the service the client wants to access.
4. The Key Distribution Center (KDC) verifies the TGT of the user and that the user has access to the service, then sends a valid session key for the service to the client.
5. The client requests the service and sends the valid session key to prove the user has access.
6. The service grants access

### Kerberos Tickets Overview

The main ticket that we will see is a ticket-granting ticket these can come in various forms such as a .kirbi for Rubeus .ccache for Impacket. The main ticket that we will see is a .kirbi ticket. A ticket is typically base64 encoded and can be used for various attacks. The ticket-granting ticket is only used with the KDC in order to get service tickets. Once we give the TGT the server then gets the User details, session key, and then encrypts the ticket with the service account NTLM hash. Our TGT then gives the encrypted timestamp, session key, and the encrypted TGT. The KDC will then authenticate the TGT and give back a service ticket for the requested service. A normal TGT will only work with that given service account that is connected to it however a KRBTGT allows us to get any service ticket that we want allowing us to access anything on the domain that we want.

Attack Privilege Requirements -

* Kerbrute Enumeration - No domain access required&#x20;
* Pass the Ticket - Access as a user to the domain required
* Kerberoasting - Access as any user required
* AS-REP Roasting - Access as any user required
* Golden Ticket - Full domain compromise (domain admin) required&#x20;
* Silver Ticket - Service hash required&#x20;
* Skeleton Key - Full domain compromise (domain admin) required

## Task 2

[Kerbrute](https://github.com/ropnop/kerbrute) is an enumeration tool used to brute-force and enumerate valid AD users by abusing the Kerberos pre-authentication.&#x20;

We \*may\* need to add the DNS domain name along with the machine IP to /etc/hosts inside of out attacker machine or these attacks will not work for us - `(IP) CONTROLLER.local`

### Abusing Pre-Authentication Overview

By brute-forcing Kerberos pre-authentication, we do not trigger the "account failed to log on" event which can cause red flags to blue teams/defenders. When brute-forcing through Kerberos we can brute-force by only sending a single UDP frame to the KDC, allowing us to enumerate the users on the domain from a wordlist or dictionary.

### Kerbrute Installation

1\. Download a precompiled binary for our OS [here](https://github.com/ropnop/kerbrute/releases). I'm running Kubuntu 20.04

2\. As I am doing this on my own machine I created a folder in the /opt/ directory and moved the file there. `cd /opt/ && sudo mkdir kerbrute && sudo mv ~/Downloads/kerbrute_linux_amd64 .`

3\. `cd /opt/kerbrute && sudo mv kerbrute_linux_amd64 kerbrute`

3\. `chmod +x kerbrute`

### Enumerating Users w/ Kerbrute

Enumerating users allows us to know which user accounts are on the target domain and which accounts could potentially be used to access the network.

`./kerbrute userenum --dc (IP) -d (IP) User.txt` - This will brute force user accounts from a domain controller using a supplied wordlist

\*For the sake of brevity I followed the rooms guide and added the machines IP to my /etc/hosts file temporarily.

![](<../../.gitbook/assets/image (184).png>)

### Question 1: How many total users do we enumerate?

`10`

### Question 2: What is the SQL service account name?

`SQLService`

### Question 3: What is the second "machine" account name?

`Machine2`

### Question 4:What is the third "user" account name?

`User3`&#x20;

## Task 3

To start this task we will need SSH into the machine, the credentials are:

* Username: `Administrator`&#x20;
* Password: `P@$$W0rd`&#x20;
* Domain: `controller.local`

[Rubeus](https://github.com/GhostPack/Rubeus) is a tool for attacking Kerberos. It is an adaptation of the kekeo tool and developed by HarmJ0y the very well known active directory guru.

**From the THM Room:** "Rubeus has a wide variety of attacks and features that allow it to be a very versatile tool for attacking Kerberos. Just some of the many tools and attacks include overpass the hash, ticket requests and renewals, ticket management, ticket extraction, harvesting, pass the ticket, AS-REP Roasting, and Kerberoasting.

The tool has way too many attacks and features for me to cover all of them so I'll be covering only the ones I think are most crucial to understand how to attack Kerberos however I encourage you to research and learn more about Rubeus and its whole host of attacks and features [here](https://github.com/GhostPack/Rubeus)."



After SSHing into the machine and going into the `Downloads` folder, running `dir`, we see `Rubeus.exe` in there. We can follow the room the find our answers.

They have run `echo MACHINE_IP CONTROLLER.local >> C:\Windows\System32\drivers\etc\hosts` to add the IP and domain name to the hosts file.

Then simply run `Rubeus.exe brute /password:Password1 /noticket` from the Downloads folder.

### Question 1: Which domain admin do we get a ticket for when harvesting tickets?

`Administrator`

### Question 2: Which domain controller do we get a ticket for when harvesting tickets?

`Controller-1`

## Task 4

Kerberoasting allows a user to request a service ticket for any service with a registered SPN then use that ticket to crack the service password. If the service has a registered SPN then it can be Kerberoastable however the success of the attack depends on how strong the password is and if it is trackable as well as the privileges of the cracked service account.

There are other tools out there such a kekeo and Invoke-Kerberoast, and Impacket.

You can follow either method here, as I was already SSHd into the machine, I went ahead and used Rubeus to obtain the hashes using `Rubeus.exe kerberoast`.

Copy the hashes to a .txt file and begin the cracking with hashcat.

### Question 1: What is the HTTPService Password?

`Summer2020`

![](<../../.gitbook/assets/image (148).png>)

### Question 2: What is the SQLService Password?

`MYpassword123#`

![](<../../.gitbook/assets/image (141).png>)

## Task 5

Very similar to Kerberoasting, AS-REP Roasting dumps the krbasrep5 hashes of user accounts that have Kerberos pre-authentication disabled. Unlike Kerberoasting these users do not have to be service accounts the only requirement to be able to AS-REP roast a user is the user must have pre-authentication disabled.

Like before. there are other tools for AS-REP Roasting such as kekeo and Impacket's GetNPUsers.py. Rubeus is easier to use because it automatically finds AS-REP Roastable users whereas with GetNPUsers we have to enumerate the users beforehand and know which users may be AS-REP Roastable.

### AS-REP Roasting Overview

During pre-authentication, the users hash will be used to encrypt a timestamp that the domain controller will attempt to decrypt to validate that the right hash is being used and is not replaying a previous request. After validating the timestamp the KDC will then issue a TGT for the user. If pre-authentication is disabled we can request any authentication data for any user and the KDC will return an encrypted TGT that can be cracked offline because the KDC skips the step of validating that the user is really who they say that they are.

After running `Rubeus.exe asreproast` we can get what is seen below

![](<../../.gitbook/assets/image (241).png>)

![](<../../.gitbook/assets/image (119).png>)

As it says in the room, be sure to Insert `23$` after `$krb5asrep$` so that the first line will be `$krb5asrep$23$User`...

### Question 1: What hash type does AS-REP Roasting use?

`Kerberos 5 AS-REP etype 23`

![](<../../.gitbook/assets/image (151).png>)

### Question 2: Which User is vulnerable to AS-REP Roasting?

`User3`

### Question 3: What is the User's Password?

`Password3`

### Quesion 4: Which Admin is vulnerable to AS-REP Roasting?

`Admin2`

### Question 5: What is the Admin's Password?

`P@$$W0rd2`

## Task 6

Mimikatz is a very popular and powerful post-exploitation tool most commonly used for dumping user credentials inside of an active directory network however well be using mimikatz in order to dump a TGT from LSASS memory

### Pass the Ticket Overview

Pass the ticket works by dumping the TGT from the LSASS memory of the machine. The Local Security Authority Subsystem Service (LSASS) is a memory process that stores credentials on an active directory server and can store Kerberos ticket along with other credential types to act as the gatekeeper and accept or reject the credentials provided. We can dump the Kerberos Tickets from the LSASS memory just like we can dump hashes. When we dump the tickets with mimikatz it will give us a .kirbi ticket which can be used to gain domain admin if a domain admin ticket is in the LSASS memory. This attack is great for privilege escalation and lateral movement if there are unsecured domain service account tickets laying around. The attack allows us to escalate to domain admin if we dump a domain admin's ticket and then impersonate that ticket using mimikatz PTT attack allowing us to act as that domain admin. We can think of a pass the ticket attack like reusing an existing ticket were not creating or destroying any tickets here were simply reusing an existing ticket from another user on the domain and impersonating that ticket.

### Prepare Mimikatz & Dump Tickets

We will need to run the command prompt as an administrator: use the same credentials as we did to get into the machine. If we don't have an elevated command prompt mimikatz will not work properly.

1.) Navigate to the directory mimikatz is in

2.) `mimikatz.exe`

3.) `privilege::debug` - Ensure this outputs \[output '20' OK] if it does not that means we do not have the administrator privileges to properly run mimikatz

![](<../../.gitbook/assets/image (152).png>)

`sekurlsa::tickets /export` - this will export all of the `.kirbi` tickets into the directory that we are currently in. Since we ran this from the Downloads folder, they will be in there.

At this step we can also use the base 64 encoded tickets from Rubeus that we harvested earlier

![](<../../.gitbook/assets/image (242).png>)

When looking for which ticket to impersonate the room recommends looking for an administrator ticket from the krbtgt, similar to the one above.

### Pass the Ticket w/ Mimikatz

Now that we have our ticket ready we can now perform a pass the ticket attack to gain domain admin privileges.

* `kerberos::ptt <ticket>` - run this command with the ticket that we harvested from earlier. It will cache and impersonate the given ticket

![](<../../.gitbook/assets/image (126).png>)

* `klist` - Here we are just verifying that we successfully impersonated the ticket by listing our cached tickets. This is not run from inside mimikatz, so be sure to exit it.

![](<../../.gitbook/assets/image (446).png>)

* We now have impersonated the ticket giving us the same rights as the TGT we are impersonating. To verify this we can look at the admin share.

![](<../../.gitbook/assets/image (382).png>)

\*Note that this is only a POC to understand how to pass the ticket and gain domain admin the way that we approach passing the ticket may be different based on what kind of engagement we are in so do not take this as a definitive guide of how to run this attack.

### Pass the Ticket Mitigation

Don't let domain admins log onto anything except the domain controller - This is something so simple however a lot of domain admins still log onto low-level computers leaving tickets around that we can use to attack and move laterally with.

## Task 7

Mimikatz is a post-exploitation tool most commonly used for dumping user credentials inside of an active directory network however well be using mimikatz in order to create a silver ticket.

A silver ticket can sometimes be better used in engagements rather than a golden ticket because it is a little more discreet. If stealth and staying undetected matter then a silver ticket is probably a better option than a golden ticket however the approach to creating one is the exact same. The key difference between the two tickets is that a silver ticket is limited to the service that is targeted whereas a golden ticket has access to any Kerberos service.

### KRBTGT Overview

A KRBTGT is the service account for the KDC. This is the Key Distribution Center that issues all of the tickets to the clients. If we impersonate this account and create a golden ticket from the KRBTGT we give our self the ability to create a service ticket for anything we want.&#x20;

A TGT is a ticket to a service account issued by the KDC and can only access that service the TGT is from like the SQLService ticket.

### Golden/Silver Ticket Attack Overview

A golden ticket attack works by dumping the ticket-granting ticket of any user on the domain. This would preferably be a domain admin, but for a golden ticket we would dump the krbtgt ticket, and for a silver ticket, we would dump any service or domain admin ticket.&#x20;

This will provide us with the service/domain admin account's security identifier (SID), that is a unique identifier for each user account, as well as the NTLM hash. We can then use these details inside of a mimikatz golden ticket attack in order to create a TGT that impersonates the given service account information.

### Question 1: What is the SQLService NTLM Hash?

`cd40c9ed96265531b21fc5b1dafcfb0a`

running `lsadump::lsa /inject /name:sqlservice` will give us our answer.

![](<../../.gitbook/assets/image (129).png>)

### Question 2: What is the Administrator NTLM Hash?

`2777b7fec870e04dda00cd7260f7bee6`

Ruunning `lsadump::lsa /inject /name:Administrator` will give us our answer.

![](<../../.gitbook/assets/image (159).png>)

## Task 8

Unlike the golden and silver ticket attacks, a Kerberos backdoor is much more subtle because it acts similar to a rootkit by implanting itself into the memory of the domain forest allowing itself access to any of the machines with a master password.&#x20;

The Kerberos backdoor works by implanting a skeleton key that abuses the way that the AS-REQ validates encrypted timestamps. A skeleton key only works using Kerberos RC4 encryption.&#x20;

The default hash for a mimikatz skeleton key is _`60BA4FCADC466C7A033C178194C03DF6`_ which makes the password `mimikatz`

### Skeleton Key Overview

The timestamp is encrypted with the users NT hash. The domain controller then tries to decrypt this timestamp with the users NT hash, once a skeleton key is implanted the domain controller tries to decrypt the timestamp using both the user NT hash and the skeleton key NT hash allowing us access to the domain forest.

Installing the Skeleton Key w/ mimikatz - From mimikatz:

`misc::skeleton`

![](<../../.gitbook/assets/image (110).png>)

### Accessing the forest

The default credentials will be `mimikatz`

Eg. `net use c:\\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz` - The share will now be accessible without the need for the Administrators password

Eg. `dir \\Desktop-1\c$ /user:Machine1 mimikatz` - access the directory of Desktop-1 without ever knowing what users have access to Desktop-1

The skeleton key will not persist by itself because it runs in the memory, but it can be scripted or persisted using other tools and techniques.
