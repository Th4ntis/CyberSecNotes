# Active Directory (AD)

## Active Directory (AD)

> Conceptual reference for how Active Directory is structured and why each component matters. For the hands-on enumeration and attack commands, see **Windows-Offense.md**; for the log events these actions generate, see **Windows-Defense.md**.

### Contents

* What is Active Directory?
* Why organizations use AD
* Domain Controllers
* The AD DS Data Store
* The Forest, Trees, and Domains
* Users
* Groups
* Default Security Groups
* Domain Trusts
* Domain Policies (GPOs)
* Domain Services
* Authentication: NTLM and Kerberos
* Azure AD / Entra ID
* Why AD matters to an attacker

***

### What is Active Directory?

Active Directory (AD) is Microsoft's directory service for Windows domain networks. It is a collection of machines and servers connected inside of **domains**, which are themselves a collective part of a bigger **forest** of domains that make up the AD network. In practical terms, AD is the central database and set of services that answers three questions for every resource on the network: _who are you_ (authentication), _what are you allowed to do_ (authorization), and _where do you belong_ (directory/organization).

The major building blocks of AD are:

* **Domain Controllers (DCs)** - the servers that run AD.
* **Forests, Trees, and Domains** - the hierarchy that organizes the network.
* **Users and Groups** - the security principals (accounts) and the collections that permissions are assigned to.
* **Trusts** - the relationships that let one domain's users reach another domain's resources.
* **Policies (GPOs)** - the rules pushed down to machines and users.
* **Domain Services** - the network services a DC offers (DNS, LDAP, etc.).

### Why organizations use AD

Most medium and large companies use AD because it allows centralized control and monitoring of every computer through a single, replicated directory rather than configuring each machine by hand. Concretely, it gives them:

* **Single sign-on / roaming** - a user can log in to _any_ authorized computer on the network and reach their stored files, folders, and settings, because identity lives in the directory rather than on the local machine. No need to create a separate local account on every workstation.
* **Centralized policy** - an administrator can enforce password rules, software installs, firewall settings, and hundreds of other options across thousands of machines from one place (see Domain Policies).
* **Centralized administration** - provisioning or disabling an employee is one change in one directory, not a visit to every device.

This convenience is exactly what makes AD a high-value target: compromise the directory (specifically, a Domain Controller) and you effectively own every identity and machine it governs.

### Domain Controllers

A **Domain Controller (DC)** is a Windows Server that has the **Active Directory Domain Services (AD DS)** role installed and has been _promoted_ to a domain controller. DCs are the center of AD - they control the rest of the domain. A DC's core responsibilities are:

* Hosting the **AD DS data store** (the directory database - see below).
* Handling **authentication and authorization** for the domain (validating logons via Kerberos and NTLM, issuing Kerberos tickets).
* **Replicating** directory updates to and from the other domain controllers in the forest, so every DC holds a consistent copy.
* Providing administrators a point to **manage domain resources** (users, groups, policies, etc.).

Because every DC holds a full, writable copy of the domain database (unless it is a Read-Only Domain Controller), gaining administrative access to _any_ writable DC is generally equivalent to owning the whole domain.

### The AD DS Data Store

The AD DS data store holds the databases and processes needed to store and manage\
directory information such as users, groups, and services. Key facts:

* Its central file is **`NTDS.dit`** - the database that contains all information for the Active Directory domain, **including the password hashes for every domain account**. This is why `NTDS.dit` (or a live extraction of its secrets) is a primary objective of domain attacks.
* It is stored by default in **`%SystemRoot%\NTDS`** (i.e. `C:\Windows\NTDS`).
* It is accessible only by the domain controller itself - the file is locked while AD DS is running, which is why attackers use techniques such as Volume Shadow Copy, `ntdsutil`, or DCSync to read its contents.

### The Forest, Trees, and Domains

The **forest** is the top-level container that holds everything together. It is the security and trust boundary of an Active Directory deployment: without the forest, the trees and domains inside it would have no common context to interact.

> **Note on the word "forest":** don't read it too literally. "Forest" is a way\
> of describing the logical connection created between a set of trees and domains
>
> * it is as much a conceptual grouping as it is a physical collection of servers.

A forest is a collection of one or more **domain trees**, and consists of:

* **Trees** - a hierarchy of one or more domains that share a contiguous DNS namespace (e.g. `corp.com`, `eu.corp.com`, `us.corp.com`).
* **Domains** - the primary unit used to group and manage objects and apply policy. A domain is itself an administrative and replication boundary.
* **Organizational Units (OUs)** - containers _inside_ a domain for grouping users, computers, printers, groups, and other OUs. OUs are the usual target for linking Group Policy and for delegating administration.
* **Trusts** - relationships that allow users to access resources in other domains (see Domain Trusts).
* **Objects** - the things stored in the directory: users, groups, computers, printers, shares, etc.
* **Domain Services** - services the DC provides, such as DNS, LLMNR, and IPv6 name resolution.
* **Domain Schema** - the ruleset that defines every object type and attribute that is allowed to exist in the forest.

**Hierarchy at a glance:** `Forest → Tree(s) → Domain(s) → OU(s) → Objects`.

### Users

Users are core to AD - without users there would be little reason to have a directory at all. There are four main account types you will commonly encounter, though organizations can define more depending on how they delegate permissions:

* **Domain Admins** - control the domain and are (with Enterprise Admins) among the only accounts with administrative access to the domain controllers. These are the crown-jewel accounts in most engagements.
* **Service Accounts** (can also be Domain Admins) - accounts tied to a service rather than a person. Windows requires them to run services such as SQL Server. They are rarely logged into interactively, often have stale passwords, and are frequently over-privileged, which makes them a common attack path (e.g. Kerberoasting).
* **Local Administrators** - can administer a specific local machine (and sometimes its local users), but **cannot** access the domain controller or manage the domain.
* **Domain Users** - ordinary everyday accounts. They log in to the machines they are authorized to use and may hold local administrator rights on specific hosts depending on the organization. They are the most numerous accounts and the usual starting point (initial foothold) for an attacker.

### Groups

**Groups** make it easier to assign permissions by bundling users and objects together and granting rights to the group rather than to each member. There are two overarching types:

* **Security Groups** - used to assign permissions/rights to many users at once. These are the groups that matter most for access control.
* **Distribution Groups** - used for email distribution lists only; they carry no security permissions. They are less directly useful to an attacker, but are still valuable during enumeration because they reveal organizational structure and valid account names.

Groups also have a **scope** (Domain Local, Global, Universal) that governs where their membership and permissions apply across domains in a forest - relevant when reasoning about trusts and cross-domain access.

### Default Security Groups

AD ships with many built-in security groups. A brief outline of commonly referenced ones (the high-value targets are called out in **bold**):

* **Domain Admins** - designated administrators of the domain. _Primary target._
* **Enterprise Admins** - designated administrators of the entire forest. _Highest-value target; can administer every domain._
* **Schema Admins** - can modify the AD schema (forest-wide object definitions).
* **Administrators** / **Domain Controllers** - the DCs themselves, and local admins of the domain.
* Domain Users - all domain users.
* Domain Guests - all domain guests.
* Domain Computers - all workstations and servers joined to the domain.
* **DNS Admins** - the DNS administrators group; historically abusable to load a\
  malicious DLL on a DC.
* DNS Update Proxy - clients permitted to perform dynamic DNS updates on behalf\
  of other clients (e.g. DHCP servers).
* Allowed RODC Password Replication Group - members whose passwords _may_ be\
  replicated to read-only domain controllers.
* Denied RODC Password Replication Group - members whose passwords may **not** be\
  replicated to any RODC.
* **Group Policy Creator Owners** - members can create/modify Group Policy for the\
  domain. _GPO abuse is a powerful lateral/privilege path._
* **Protected Users** - members receive additional protections against\
  authentication-based attacks (e.g. no NTLM, no DES/RC4 Kerberos, no credential\
  delegation). ([Microsoft reference](http://go.microsoft.com/fwlink/?LinkId=298939))
* Cert Publishers - members may publish certificates to the directory.
* Read-Only Domain Controllers / Enterprise Read-Only Domain Controllers - the\
  RODCs of the domain / forest.
* **Key Admins** / **Enterprise Key Admins** - can perform administrative actions\
  on key objects (relevant to Windows Hello / credential key material).
* Cloneable Domain Controllers - DCs in this group may be cloned.
* RAS and IAS Servers - servers permitted to read remote-access properties of\
  users.

### Domain Trusts

**Trusts** are the mechanism that lets users in one domain access resources in another. For the most part, trusts define how the domains inside a forest communicate; in some environments trusts are extended out to external domains and even to other forests.

Two properties describe how a trust behaves:

* **Direction** - a trust flows from a **trusting** domain to a **trusted** domain. A _one-way_ trust lets one side access the other but not vice versa; a _two-way_ (bidirectional) trust lets both.
* **Transitivity** - a **transitive** trust extends beyond the two directly linked domains to include other domains those domains trust; a **non-transitive** trust is limited to just the two endpoints.

The combination of direction and transitivity determines how domains and trees in\
a forest can pass authentication and data between each other. Attackers can abuse\
trust relationships (for example, forging inter-realm Kerberos tickets or abusing\
SID history) to **move laterally** and escalate across domain and even forest\
boundaries.

### Domain Policies (GPOs)

Policies are a very large part of AD: they dictate how machines and users in the\
domain behave and what rules they must follow. A useful mental model is that\
**Group Policy Objects (GPOs) are to rules what groups are to permissions** -\
except that instead of applying only to a set of users, a policy can apply to an\
entire domain, site, or OU.

GPOs act as a centrally managed rulebook that a domain admin can modify as needed\
to keep the network running smoothly and securely. Alongside a long list of\
default policies, admins can author their own. For example, to disable Windows\
Defender on every machine, an admin could create a GPO that does so domain-wide.

Because GPOs are so powerful and far-reaching, they are a major focus for\
attackers enumerating a network - both to understand the environment's security\
posture and because **write access to a GPO linked to many machines is a direct**\
**path to mass code execution.** A couple of illustrative policies:

* **Disable Windows Defender** - turns off Defender across all machines in scope.
* **Digitally Sign Communications (Always)** - enables/disables SMB signing,\
  which affects susceptibility to relay attacks.

### Domain Services

Domain services are the network services a domain controller provides to the rest\
of the domain or tree. Many services can be added; the common defaults include:

* **LDAP** (Lightweight Directory Access Protocol) - the protocol applications use\
  to query and communicate with the directory. The primary interface for AD\
  enumeration.
* **Certificate Services (AD CS)** - lets the domain create, validate, and revoke\
  public-key certificates. Misconfigured certificate templates (the "ESC"\
  techniques) are a well-known privilege-escalation surface.
* **DNS, LLMNR, NBT-NS** - name-resolution services mapping hostnames to IPs.\
  LLMNR and NBT-NS in particular are frequently abused for credential-poisoning /\
  relay attacks (e.g. with Responder).

### Authentication: NTLM and Kerberos

Authentication is simultaneously the most important and the most frequently\
attacked part of AD. Two protocols dominate:

* **Kerberos** - the default authentication protocol for modern Active Directory.\
  It uses **ticket-granting tickets (TGTs)** and **service tickets (TGS)** issued\
  by the DC's Key Distribution Center to authenticate users and grant access to\
  resources without resending the password. Its ticket model is the basis for\
  attacks such as **Kerberoasting**, **AS-REP roasting**, **Golden/Silver**\
  **tickets**, and **delegation abuse**.
* **NTLM** - the legacy Windows authentication protocol, using an encrypted\
  challenge/response handshake. It underpins **pass-the-hash** and **NTLM relay**\
  attacks and remains enabled in most environments for backward compatibility.

> The domain's authentication services are the main access point for attackers and\
> include some of AD's most abused protocols - this will not be the last time they\
> come up in the context of AD security. For the hands-on side, see the\
> **Attacking Kerberos** room on TryHackMe\
> ([https://tryhackme.com/room/attackingkerberos](https://tryhackme.com/room/attackingkerberos)).
>
> _(Note: an earlier version of these notes linked to a local_\
> _`kerberos-and-kerberoasting.md` file that no longer exists in this vault - the_\
> _&#x54;ryHackMe room above is the live reference.)_

### Azure AD / Entra ID

Azure AD (now branded **Microsoft Entra ID**) acts as a cloud identity layer\
sitting between an organization's on-premises Active Directory and its users'\
sign-ins. By brokering authentication through hardened cloud protocols, it makes\
many classic on-prem AD attacks ineffective - though it introduces its own cloud\
attack surface (token theft, consent phishing, misconfigured app registrations,\
etc.). It is a complement to, not simply a drop-in replacement for, on-prem AD.

#### On-prem AD vs. Azure AD at a glance

The clearest way to see how cloud identity differs from a traditional on-prem\
network is a side-by-side of the technologies each uses:

| Windows Server AD   | Azure AD (Entra ID) |
| ------------------- | ------------------- |
| LDAP                | REST APIs           |
| NTLM                | OAuth 2.0 / SAML    |
| Kerberos            | OpenID Connect      |
| OU tree             | Flat structure      |
| Domains and Forests | Tenants             |
| Trusts              | Guests (B2B)        |

The takeaway: on-prem AD and Azure AD solve the same problem (identity and access)\
but with fundamentally different protocols and structures, so the enumeration and\
attack techniques differ substantially between them.

### Why AD matters to an attacker

Pulling the pieces together, AD is attractive to an attacker because it\
_&#x63;entralizes_ trust:

* A single compromised **Domain User** is often enough to begin enumerating the\
  entire directory over LDAP.
* **Service accounts**, **GPO write access**, **trust relationships**, and\
  **AD CS** each offer a route to escalate privilege or move laterally.
* The ultimate objective is usually a **Domain Controller** / the secrets in\
  **`NTDS.dit`**, after which the attacker controls every identity in the domain.

Keep this "centralized trust" theme in mind - nearly every AD attack is some way\
of abusing a trust relationship the directory was designed to provide.
