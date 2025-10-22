# Active Directory

### What is Active Directory?

Active Directory (AD) is a collection of machines and servers connected inside of domains, that are a collective part of a bigger forest of domains, that make up the AD network.&#x20;

Various pieces of AD:&#x20;

* Domain Controllers (DC)
* Forests, Trees, Domains
* Users + Groups&#x20;
* Trusts
* Policies&#x20;
* Domain Services

### Why use Active Directory?

Most large companies use AD because it allows for control and monitoring of their computers through a single domain controller(DC). It allows users to sign in to any computer on the AD network and have access to their stored files and folders in the server, as well as the local storage on that machine. This allows for any user in the company to use any machine that the company owns, without having to set up multiple users on a machine.

### Domain Controllers

﻿A domain controller (DC) is a Windows server that has Active Directory Domain Services (AD DS) installed and has been promoted to a domain controller. DCs are the center of AD, they control the rest of the domain. DC Tasks are typically:

* Holds the AD DS data store&#x20;
* Handles authentication and authorization services&#x20;
* Replicate updates from other domain controllers in the forest
* Allows admin access to manage domain resources

### AD DS Data Store

The Active Directory Data Store holds the databases and processes needed to store and manage directory information such as users, groups, and services. Some of the contents and characteristics of the AD DS Data Store:

* Contains the `NTDS.dit` - a database that contains all of the information of an Active Directory domain controller as well as password hashes for domain users
* Stored by default in `%SystemRoot%\NTDS`
* Accessible only by the domain controller

### The Forest

The forest is what defines everything. It is the container that holds all of the other bits and pieces of the network together. Without the forest all of the other trees and domains would not be able to interact.

**\*Note:** when thinking of the forest is to not think of it too literally. It is a physical thing just as much as it is a figurative thing. When we say "forest", it is only a way of describing the connection created between these trees and domains by the network.

### Forest Overview

﻿﻿A forest is a collection of one or more domain trees inside of an AD network. It is what categorizes the parts of the network as a whole.

The Forest consists of:

* Trees - A hierarchy of domains in Active Directory Domain Services
* Domains - Used to group and manage objects&#x20;
* Organizational Units (OUs) - Containers for groups, computers, users, printers and other OUs
* Trusts - Allows users to access resources in other domains
* Objects - users, groups, printers, computers, shares
* Domain Services - DNS Server, LLMNR, IPv6
* Domain Schema - Rules for object creation

### Users Overview

﻿Users are the core to AD, without users why have AD in the first place? There are four main types of users we'll find in an AD network, but, there can be more depending on how a company manages the permissions of its users.

The four types of users are:&#x20;

* Domain Admins - They control the domains and are the only ones with access to the domain controller.
* Service Accounts (Can be Domain Admins) - These are for the most part never used except for service maintenance, they are required by Windows for services, such as SQL ,to pair a service with a service account
* Local Administrators - These users can make changes to local machines as an administrator and may even be able to control other normal users, but they cannot access the domain controller
* Domain Users - These are our everyday users. They can log in on the machines they have the authorization to access and may have local administrator rights to machines depending on the organization.

### Groups Overview

﻿Groups make it easier to give permissions to users and objects by organizing them into groups with specified permissions. There are two overarching types of AD groups:&#x20;

* Security Groups - These groups are used to specify permissions for a large number of users
* Distribution Groups - These groups are used to specify email distribution lists. As an attacker these groups are less beneficial to us but can still be beneficial in enumeration

### Default Security Groups

﻿There are a lot of default security groups. Here is a brief outline of just a few security groups:

* Domain Controllers - All domain controllers in the domain
* Domain Guests - All domain guests
* Domain Users - All domain users
* Domain Computers - All workstations and servers joined to the domain
* Domain Admins - Designated administrators of the domain
* Enterprise Admins - Designated administrators of the enterprise
* Schema Admins - Designated administrators of the schema
* DNS Admins - DNS Administrators Group
* DNS Update Proxy - DNS clients who are permitted to perform dynamic updates on behalf of some other clients, such as DHCP servers
* Allowed RODC Password Replication Group - Members in this group can have their passwords replicated to all read-only domain controllers in the domain
* Group Policy Creator Owners - Members in this group can modify group policy for the domain
* Denied RODC Password Replication Group - Members in this group cannot have their passwords replicated to any read-only domain controllers in the domain
* Protected Users - Members of this group are afforded additional protections against authentication security threats. [This link](http://go.microsoft.com/fwlink/?LinkId=298939) has more information.
* Cert Publishers - Members of this group are permitted to publish certificates to the directory
* Read-Only Domain Controllers - Members of this group are Read-Only Domain Controllers in the domain
* Enterprise Read-Only Domain Controllers - Members of this group are Read-Only Domain Controllers in the enterprise
* Key Admins - Members of this group can perform administrative actions on key objects within the domain.
* Enterprise Key Admins - Members of this group can perform administrative actions on key objects within the forest.
* Cloneable Domain Controllers - Members of this group that are domain controllers may be cloned.
* RAS and IAS Servers - Servers in this group can access remote access properties of users

### Domain Trusts Overview

﻿Trusts are a mechanism in place for users in the network to gain access to other resources in the domain. For the most part, trusts outline the way that the domains inside of a forest communicate to each other. In some environments trusts can be extended out to external domains and even forests in some cases.

There are two types of trusts that determine how the domains communicate:

* Directional - The direction of the trust flows from a trusting domain to a trusted domain
* Transitive - The trust relationship expands beyond just two domains to include other trusted domains

The type of trusts put in place determines how the domains and trees in a forest are able to communicate and send data to and from each other. Attackers can sometimes abuse these trusts in order to move laterally throughout the network.&#x20;

### Domain Policies Overview

Policies are a very big part of AD, they dictate how the server operates and what rules it will and will not follow. We can think of domain policies like domain groups, except instead of permissions they contain rules, and instead of only applying to a group of users, the policies apply to a domain as a whole.&#x20;

They simply act as a rulebook for AD that a domain admin can modify and alter as they see necessary to keep the network running smoothly and securely. Along with the very long list of default domain policies, domain admins can choose to add in their own policies not already on the domain controller. For example, if we wanted to disable windows defender across all machines on the domain we could create a new group policy object to disable Windows Defender.

The options for domain policies are almost endless and are a big factor for attackers when enumerating an AD network. A couple example policies are:&#x20;

* Disable Windows Defender - Disables windows defender across all machine on the domain
* Digitally Sign Communication (Always) - Can disable or enable SMB signing on the domain controller

### Domain Services Overview

Domain Services are services that the domain controller provides to the rest of the domain or tree. There is a wide range of various services that can be added to a domain controller. Here are the default domain services:&#x20;

* LDAP - Lightweight Directory Access Protocol; provides communication between applications and directory services
* Certificate Services - allows the domain controller to create, validate, and revoke public key certificates
* DNS, LLMNR, NBT-NS - Domain Name Services for identifying IP hostnames

### Domain Authentication Overview

The most important part of AD, as well as the most vulnerable part of AD, is the authentication protocols set in place. There are two main types of authentication in place for AD: NTLM and Kerberos. For more information on NTLM and Kerberos check out the [Attacking Kerberos room](https://tryhackme.com/room/attackingkerberos) on TrYHackMe as well as my notes on [Kerberos here](broken-reference).

* Kerberos - The default authentication service for Active Directory uses ticket-granting tickets and service tickets to authenticate users and give users access to other resources across the domain.
* NTLM - default Windows authentication protocol uses an encrypted challenge/response protocol

The AD domain services are the main access point for attackers and contain some of the most vulnerable protocols for Active Directory, this will not be the last time we see them mentioned in terms of Active Directory security.

### Azure AD Overview

﻿Azure acts as the middle man between our physical Active Directory and our users' sign on. This allows for a more secure transaction between domains, making a lot of Active Directory attacks ineffective.

### Cloud Security Overview

The best way to show us how the cloud takes security precautions past what is already provided with a physical network is to show a comparison with a cloud Active Directory environment:&#x20;

| **Windows Server AD** | **Azure AD**   |
| --------------------- | -------------- |
| LDAP                  | Rest APIs      |
| NTLM                  | OAuth/SAML     |
| Kerberos              | OpenID         |
| OU Tree               | Flat Structure |
| Domains and Forests   | Tenants        |
| Trusts                | Guests         |



