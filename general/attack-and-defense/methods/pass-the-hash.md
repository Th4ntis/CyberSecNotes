# Pass-The-Hash

A **Pass-the-Hash (PtH) attack** is a technique whereby an attacker captures a password hash (as opposed to the password characters) and then simply passes it through for authentication and potentially lateral access to other networked systems. The threat actor doesn’t need to decrypt the hash to obtain a plain text password. PtH attacks exploit the authentication protocol, as the passwords hash remains static for every session until the password is rotated. Attackers commonly obtain hashes by scraping a system’s active memory and other techniques.

While Pass-the-Hash attacks can occur on Linux, Unix, and other platforms, they are most prevalent on Windows systems. In Windows, PtH exploits Single Sign-On (SS0) through NT Lan Manager (NTLM), Kerberos, and other authentication protocols. When a password is created in Windows, it is hashed and stored in the Security Accounts Manager (SAM), Local Security Authority Subsystem (LSASS) process memory, the Credential Manager (CredMan) store, a ntds.dit database in Active Directory, or elsewhere. When a user logs onto a Windows workstation or server, they essentially leave behind their password credentials.

This is primarily a lateral movement technique. This means that attackers are using pass the hash to extract additional information and credentials after already compromising a device. By laterally moving between devices and accounts, attackers can use pass the hash to gain the right credentials to eventually escalate their domain privileges and access more influential systems, such as an administrator account on the domain controller. Most of the movement executed during a pass the hash attack uses a remote software program.

### Pass-The-Hash Process

To execute a pass the hash attack, the attacker first obtains the hashes from the targeted system using any number of hash-dumping tools, such as hashdump, mimikatz, etc. The attacker then uses these tools to place the obtained hashes on a Local Security Authority Subsystem Service (LSASS).

These attacks are often directed at Windows machines due to the security vulnerability of the New Technology Local Area Network Manager (NTLM) hashes once admin privileges have been obtained. These attacks often trick a Windows-based authentication system into believing that the attacker's endpoint is that of the legitimate user and will automatically provide the required credentials when the attacker tries to access the targeted system. This can all be accomplished without any need for the original password.

The NTLM hashes, fixed-length mathematical codes derived from the passwords, are the key to pass the hash attacks. They enable the attacker to use compromised domain accounts without extracting the plaintext password or having to decrypt the hash. This is because computer OSs, such as Windows, never actually send or save user passwords over their network. Instead, these systems store passwords as encrypted NTLM hashes, which represent the password but can't be reverse-engineered.

NTLM can still be used in place of the password to access various accounts and resources on the network. For an attacker to be able to access the LSASS, they need to successfully compromise a computer to the point where the malware can run with local admin rights.

Once a Windows-based machine is compromised and the deployed malware is granted access to the local usernames and NTLM hashes, the attacker can choose whether to hunt for more credentials or attempt to access network resources using the credentials of elevated users.

For example, by gathering more user credentials, an attacker can retrieve the credentials of users who either have separate accounts on the Windows machine, such as a service account, or have remote access to the computer as a logon administrator. Remote admins who log onto the compromised Windows machine will expose their username and NTLM hash to the now integrated malware. An attacker who has an IT administrator's credentials can move laterally through networked devices.

Lateral movement is an effective way to search for users with elevated privileges, such as administrative rights to protected resources. Privilege escalation can be obtained by finding the credentials of an administrator with greater administrative access. For example, a pass the hash attacker could locate the login credentials of the domain administrator through lateral movement. Recognizing their elevated privileges, attackers can start running processes as a domain administrator on the domain controller. These elevated resources could also include customer databases, source code depositories and email servers.

## Defense

COMING SOON
