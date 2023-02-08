# Kerberos and Kerberoasting

## Kerberos

Kerberos is a network security protocol that authenticates service requests between two or more trusted hosts across an untrusted network, such as the internet. It uses secret-key cryptography and a trusted third party for authenticating client-server applications and verifying users' identities. It works on the basis of tickets to allow endpoints communicating over a non-secure network to prove their identity to one another in a secure manner.

Kerberos is found everywhere, it is employed heavily on secure systems that depend on reliable auditing and authentication features. It is used in Posix authentication, Active Directory, NFS, and Samba. It's also an alternative authentication system to SSH, POP, and SMTP.

Pros and Cons of Kerberos

Pros:

1. Secret keys are shared, which is more efficient than sharing public keys.
2. Effective Access Control: Kerberos gives users a single point to keep track of logins and security policy enforcement
3. Limited Lifetime for Key Tickets: Each Kerberos ticket has a timestamp, lifetime data, and authentication duration controlled by the administrator. If the ticket gets stolen, it is hard to reuse the ticket because of strong authentication needs.
4. Mutual Authentication: Service systems and users can authenticate each other.
5. Reusable Authentication: Kerberos user authentication is reusable and durable, requiring each user to get verified by the system just once. As long as the ticket is in effect, the user won’t have to keep entering their personal information for authentication purposes.
6. Strong and Diverse Security Measures: Kerberos security authentication protocols employ cryptography, multiple secret keys, and third-party authorization, creating a strong, secure defense. Passwords do not get sent over networks unencrypted, and all secret keys are encrypted.

Cons:

1. It is vulnerable to weak or repeated passwords.
2. It only provides authentication for services and clients.

### Kerberos Workflow:

* Client: The client acts on behalf of the user and initiates communication for a service request
* Server: The server hosts the service the user wants to access
* Authentication Server (AS): The AS performs the desired client authentication. If the authentication happens successfully, the AS issues the client a ticket called Ticket Granting Ticket (TGT). This ticket assures the other servers that the client is authenticated
* Key Distribution Center (KDC): In a Kerberos environment, the authentication server logically separated into three parts: A database, the AS, and the Ticket Granting Server (TGS). These three parts, in turn, exist in a single server called the Key Distribution Center
* Ticket Granting Server (TGS): The TGS is an application server that issues service tickets as a service

The protocol flow consists of the following steps:

**Step 1**: Initial client authentication request. The user asks for a TGT from the AS. This request includes the client ID.

**Step 2**: KDC verifies the client's credentials. The AS checks the database for the client and TGS's availability. If the AS finds both values, it generates a client/user secret key, applying the user's password hash.

The AS then calculates the TGS secret key and creates a session key (SK1) encrypted by the client/user secret key. The AS then generates a TGT containing the client ID, client network address, timestamp, lifetime, and SK1. The TGS secret key then encrypts the ticket.

**Step 3**: The client decrypts the message. The client uses the client/user secret key to decrypt the message and extract the SK1 and TGT, generating the authenticator that validates the client's TGS.

**Step 4:** The client uses TGT to request access. The client requests a ticket from the server offering the service by sending the extracted TGT and the created authenticator to TGS.

**Step 5**: The KDC creates a ticket for the file server. The TGS then uses the TGS secret key to decrypt the TGT received from the client and extracts the SK1. The TGS decrypts the authenticator and checks to see if it matches the client ID and client network address. The TGS also uses the extracted timestamp to make sure the TGT hasn't expired.

If the process conducts all the checks successfully, then the KDC generates a service session key (SK2) that is shared between the client and the target server.

Finally, the KDC creates a service ticket that includes the client id, client network address, timestamp, and SK2. This ticket is then encrypted with the server's secret key obtained from the db. The client receives a message containing the service ticket and the SK2, all encrypted with SK1.

**Step 6**: The client uses the file ticket to authenticate. The client decrypts the message using SK1 and extracts SK2. This process generates a new authenticator containing the client network address, client ID, and timestamp, encrypted with SK2, and sends it and the service ticket to the target server.

**Step 7**: The target server receives decryption and authentication.  The target server uses the server's secret key to decrypt the service ticket and extract the SK2. The server uses SK2 to decrypt the authenticator, performing checks to make sure the client ID and client network address from the authenticator and the service ticket match. The server also checks the service ticket to see if it's expired.

## Kerberoasting

Kerberoasting is an attack method that allows an attacker to take advantage of how service accounts leverage Kerberos authentication with Service Principle Names (SPN). It allows the attacker to crack the passwords of the service accounts in Active Directory. Cracking the password is often done offline to avoid being detected. While the attacker doesn't exploit any security loophole, all that is being done is using the working of the protocol to get into the network and persist.

[Attacking Kerberos](../../../personal/tryhackme/attacking-kerberos.md)

[Attacking Kerberos on TryHackMe](https://tryhackme.com/room/attackingkerberos)

### Kerberoasting Process:

**Step 1:** The first step involves scanning Active Directory for user accounts with SPN values set and `AdminCount =1`. This is done using several techniques such as PowerShell and LDAP queries, using the default scripts in Kerberoast toolkit, or using PowerSploit.

**Step 2:** After listing down the targeted accounts, request service tickets from AD using the SPN values.

**Step 3:** Extract the service tickets and hashes to the memory using tools, such as Mimikatz, and save the information to a file.

**Step 4:** Brute force the encrypted passwords to obtain the actual clear text.

**Step 5:** Using the user accounts with privileges, move laterally or cause destruction.

**Note:** It's easy to crack service accounts as their passwords rarely change. Moreover, since the cracking happens offline, it'll not cause any domain traffic or account lockouts. Hence, it is undetectable.

## Golden Ticket

A golden ticket is a forged TGT created with a stolen KDC key. A golden ticket enables the attacker to create a fake domain administrator identity to gain access to any service on a domain.

The KDC automatically trusts a TGT that is encrypted with a KDC key. But stealing the KDC key is not an easy feat. To do this, an attacker must establish themselves on the network, escalate their privileges, and compromise the DC. All of these steps require expertise and time. But this attack can be facilitated with the help of tools, such as Mimikatz or Empire, designed to exploit Kerberos.

With Mimikatz, the attacker can bypass the step of compromising the DC to steal the KRBTGT account hash (KDC key) with a technique called DCSync. With the stolen KDC key, Mimikatz helps the attacker create a golden ticket with a fake username and PAC, specifying domain administrator privileges for that username. The attacker bypasses the initial step of requesting the TGT from the KDC and directly requests a TGS ticket for a service, such as an administrative share or an important database (3). The KDC trusts the golden ticket and creates a TGS ticket with the fake PAC.

## Defense

COMING SOON
