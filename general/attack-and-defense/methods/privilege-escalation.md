---
description: Tool's for PrivEsc
---

# Privilege Escalation

Privilege escalation happens when a user exploits a bug, design flaw, or configuration error in an application or operating system to gain elevated access to resources that should normally be unavailable to them. The user can use the newly obtained privileges to steal confidential data, run administrative commands or deploy malware.&#x20;

Common Privilege Escalation attack vectors are

* Credential Exploitation
* Vulnerabilities and Exploits
* Misconfigurations
* Malware
* Social Engineering



## All Around Tools

* [PEASS-Ng](https://github.com/carlospolop/PEASS-ng) - Tools search for possible local privilege escalation paths that you could exploit and print them to you with nice colors so you can recognize the misconfigurations easily.
  * Check the Local Windows Privilege Escalation checklist [here](https://book.hacktricks.xyz/windows/checklist-windows-privilege-escalation)
  * [WinPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS) - Windows local Privilege Escalation Awesome Script (C#.exe and .bat)
  * Check the Local Linux Privilege Escalation checklist [here](https://book.hacktricks.xyz/linux-unix/linux-privilege-escalation-checklist)
  * [LinPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) - Linux local Privilege Escalation Awesome Script (.sh)

## Windows

#### _**Access Token Manipulation**_ <a href="#heading-11" id="heading-11"></a>

Windows uses access tokens to determine the owners of running processes. When a process tries to perform a task that requires privileges, the system checks who owns the process and to see if they have sufficient permissions. Access token manipulation involves fooling the system into believing that the running process belongs to someone other than the user who started the process, granting the process the permissions of the other user.

**Techniques**

There are three ways to achieve access token manipulation:

* Duplicating an access token using the Windows DuplicateToken(Ex) and then using ImpersonateLoggedOnUserfunction or SetThreadToken function to assign the impersonated token to a thread.
* Creating a new process with an impersonated token using the DuplicateToken(Ex) function together with the CreateProcessWithTokenW function.
* Leveraging username and password to create a token using the LogonUser function. The attacker possesses a username and password, and without logging on, they create a logon session, obtain the new token and ue SetThreadToken to assign it to a thread.

In this method, an adversary has a username and password, but the user is not logged

**Mitigation**

There is no way to disable access tokens in Windows. However, to perform this technique an attacker must already have administrative-level access. The best way to prevent the attack is to assign administrative rights in line with the least-privilege principle, regularly review administrative accounts and revoke them if access is no longer needed. Also, monitor privileged accounts for any sign of anomalous behavior.

#### _**Bypass User Account Control**_ <a href="#heading-12" id="heading-12"></a>

**Attack description**

The Windows user account control (UAC) mechanism creates a distinction between regular users and administrators. It limits all applications to standard user permissions unless specifically authorized by an administrator, to prevent malware from compromising the operating system. However, if UAC protection is not at the highest level, some Windows programs can escalate privileges, or execute COM objects with administrative privileges.

**Mitigation**

Review IT systems and ensure UAC protection is set to the highest level, or if this is not possible, apply other security measures. Regularly review which accounts are a local administrator group on sensitive systems and remove regular users who should not have administrative rights.

#### _**DLL Search Order Hijacking**_ <a href="#heading-13" id="heading-13"></a>

**Attack description**

Attackers can perform “DLL preloading”. This involves planting a malicious DLL with the same name as a legitimate DLL, in a location which is searched by the system before the legitimate DLL. Often this will be the current working directory, or in some cases attackers may remotely set the working directory to an external file volume. The system finds the DLL in the working folder, thinking it is the legitimate DLL, and executes it.

**Techniques**

There are several other ways to achieve DLL search order hijacking:

* Replacing an existing DLL or modifying a .manifest or .local redirection file, directory, or junction
* Performing search order DLL hijacking on a vulnerable program that has a higher privilege level, causing the attacker’s DLL to run at the same privilege level. This can be used to elevate privileges from user to administrator, or from administrator to SYSTEM.
* Covering the attack by loading the legitimate DLLS together with the malicious DLLs, so that systems appear to run as usual.

**Mitigation**

Here are several ways to prevent a DLL search order hijack:

* Disallow loading of remote DLLs
* Enable Safe DLL Search Mode to force search for system DLLs in directories with greater restrictions
* Use auditing tools such as PowerSploit to detect DLL search order hijacking vulnerabilities and correct them
* Identify and block software executed through search order hijacking, using whitelisting tools like AppLocker.

### Tools

* [WinPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS) - A script developed to enumerate the target system to uncover privilege escalation paths. You can find more information about winPEAS and download either the precompiled executable or a .bat script. **\*Note**, Windows Defender detects and disables winPEAS.
* [PowerUP](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc) - A PowerShell script that searches common privilege escalation on the target system. Able to be run with run with the `Invoke-AllChecks` option that will perform all possible checks on the target system or use it to conduct specific checks
*   [Windows Exploit Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester) - Compares a targets patch levels against the Microsoft vulnerability database in order to detect potential missing patches on the target. Notifies the user if there are public exploits and Metasploit modules available for the missing bulletins.

    It requires the 'systeminfo' command output from a Windows host in order to compare that the Microsoft security bulletin database and determine the patch level of the host.

    It has the ability to automatically download the security bulletin database from Microsoft with the --update flag, and saves it as an Excel spreadsheet.
* [Windows Exploit Suggester (Newer)](https://github.com/bitsadmin/wesng) - Tool based on the output of Windows' `systeminfo` utility which provides the list of vulnerabilities the OS is vulnerable to, including any exploits for these vulnerabilities. Every Windows OS between Windows XP and Windows 11, including their Windows Server counterparts, is supported.

## Linux&#x20;

#### _**What Is Enumeration?**_ <a href="#heading-15" id="heading-15"></a>

In Linux systems, attackers use a process called “enumeration” to identify weaknesses that may allow privilege escalation. Enumeration involves:

* Using Google searches, port scanning and direct interaction with a system to learn more about it and see how it responds to inputs.
* Seeing if compilers, or high-level programming languages like Perl or Python, are available, which can allow an attacker to run exploit code.
* Identifying software components, such as web servers and their versions.
* Retrieving data from key system directories such as /etc, /proc, ipconfig, lsof, netstat and uname.

Attackers use automated tools to perform enumeration on Linux systems. You should also use the same tools to pre-empt an attack, by scanning your own system, identifying weaknesses, and addressing them.

Below are two specific techniques for escalating privilege on Linux and how to mitigate them.

#### _**Kernel Exploit**_ <a href="#heading-16" id="heading-16"></a>

**Attack description**

From time to time, vulnerabilities are discovered in the Linux kernel. Attackers can exploit these vulnerabilities to gain root access to a Linux system, and once the system is infected with the exploit, there is no way to defend against it.

Attackers go through the following steps:

1. Learn about the vulnerabilities
2. Develop or acquire exploit code
3. Transfer the exploit onto the target
4. Execute the exploit on the target

**Mitigation**

Follow security reports and promptly install Linux updates and patches. Restrict or remove programs that enable file transfers, such as FTP, SCP, or curl, or restrict them to specific users or IPs. This can prevent transfer of an exploit onto a target device. Remove or restrict access to compilers, such as GCC, to prevent exploits from executing. You should also limit which folders are writable or executable.

#### _**Exploiting SUDO Rights**_ <a href="#heading-17" id="heading-17"></a>

**Attack description**

SUDO is a Linux program that lets users run programs with the security privileges of another user. Older versions would run as the superuser (SU) by default. Attackers can try to compromise a user who has SUDO access to a system, and if successful, they gain root privileges.

A common scenario is administrators granting access to some users to perform supposedly harmless SUDO commands, such as ‘find’. However, the ‘find’ command container parameters that enable command execution, and so if attackers compromise that user’s account, they can execute commands with root privileges.

**Mitigation**

Never give SUDO rights to the programming language compiler, interpreter or editors, including vi, more, less, nmap, perl, ruby, python, gdb. Do not give sudo rights to any program that enables running a shell. And severely limit SUDO access using the least-privilege principle.

### Tools

* [LinPeas](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS) - A script that search for possible paths to escalate privileges on Linux/Unix\*/MacOS hosts. The checks are explained [here](https://book.hacktricks.xyz/linux-unix/privilege-escalation).
* [LinEnum](https://github.com/rebootuser/LinEnum) - An older shell script will show relevant information about the security of the local Linux system, helping to escalate privileges.
* [LES (Linux Exploit Suggester)](https://github.com/mzet-/linux-exploit-suggester) - A tool is designed to assist in detecting security deficiencies for given Linux kernel/Linux-based machine.
* [Linux Smart Enumeration](https://github.com/diego-treitos/linux-smart-enumeration) - A tool based off of [LinEnum](https://github.com/rebootuser/LinEnum) and its uses. A shell script will show relevant information about the security of the local Linux system, helping to escalate privileges.
* [Linux Priv Checker](https://github.com/linted/linuxprivchecker) - Script is intended to be executed locally on a Linux box to enumerate basic system info and search for common privilege escalation vectors such as word writable files, misconfigurations, clear-text password and applicable exploits.

## Defense

COMING SOON
