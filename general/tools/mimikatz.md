# Mimikatz

Mimikatz is an incredibly effective offensive security tool developed by gentilkiwi. It is a post-exploitation tool that dumps passwords from memory, as well as hashes, PINs and Kerberos tickets. Other useful attacks are pass-the-hash, pass-the-ticket or building Golden Kerberos tickets. This makes post-exploitation lateral movement within a network easy for attackers. Mimikatz is a very powerful tool when attacking,or defending Windows Systems, it can also play with certificates or private keys, vault and more.

Mimikatz can only dump credentials and password hashes if it is executed from the context of a privilege user, like local admin.

[Mimikatz github(source)](https://github.com/gentilkiwi/mimikatz)

[Mimikatz binaries](https://github.com/gentilkiwi/mimikatz/releases/tag/2.2.0-20210810)

## Usage

Simply run the .exe as admin from where you can get the executable onto the victim machine.

![](../../../.gitbook/assets/2022-04-11\_01-24.png)

From here there is a multitude of things we can run. Examples:

* `privilege::debug` - get debug rights (this or Local System rights is required for many Mimikatz commands).
* `sekurlsa::logonpasswords`[ ](https://adsecurity.org/?page\_id=1821#SEKURLSALogonPasswords)- lists all available provider credentials. This usually shows recently logged on user and computer credentials.

![](../../../.gitbook/assets/2022-04-11\_01-29.png)

* `sekurlsa::kerberos` - List Kerberos credentials for all authenticated users (including services and computer account)
* `sekurlsa::tickets` - Lists all available Kerberos tickets for all recently authenticated users, including services running under the context of a user account and the local computer’s AD computer account. Unlike kerberos::list, sekurlsa uses memory reading and is not subject to key export restrictions. sekurlsa can access tickets of others sessions (users).
* `kerberos::golden` – create golden/silver/trust tickets
* `kerberos::list` – List all user tickets (TGT and TGS) in user memory. No special privileges required since it only displays the current user’s tickets.Similar to functionality of “klist”.
* `kerberos::ptt` – pass the ticket. Typically used to inject a stolen or forged Kerberos ticket (golden/silver/trust).
* `token::elevate` – impersonate a token. Used to elevate permissions to SYSTEM (default) or find a domain admin token on the box
* `token::elevate /domainadmin` – impersonate a token with Domain Admin credentials.

and a lot more listed on the [Mimikatz Wiki](https://github.com/gentilkiwi/mimikatz/wiki)

## Defense

COMING SOON
