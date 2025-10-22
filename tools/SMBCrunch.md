# About
3 tools that work together to simplify reconaissance of Windows File Shares. `SMBGrab.pl`, `SMBHunt.pl`, and `SMBList.pl`. 
## SMBHunt
Given a file (or gnmap file), SMBHunt finds all the Windows File Shares associated with the servers provided (if gnmap file is provided, it looks at servers with port 445 open). If no credentials are supplied to perform the check, it will check for null session shares.

**Warning: If your user has access to one share on the server, the script will show all shares hosted by that server. If a share is listed in this output, it does _not_ mean you have access to that share. Use the next tool for that.**

This script does warn you if the credentials you supply fail to avoid locking out domain accounts. "-f" switch overrides this protection.

**This script only checks a server using one credential. This is by design since the server will respond with a full list of shares if the user has access to only one share on the system**
## SMBList
SMBList will take the output file from "SMBHunt.pl" (or a file of shares separated by a newline in the format of "\server\share") and will perform a recursive directory listing of those shares using the credentials provided. SMBList will attempt to authenticate to the share until a valid credential is found from the list provided. It will then store the directory listings in a subfolder specified.

This makes the file listing extremely easy to grep through!

** The best result file to use is: /ALL_COMBINED_RESULTS.txt **
## SMBGrab
File listings from SMBList.pl can be pipped into this utility to grab the files wanted from the shares. The original listing from SMBList.pl should be "grepped" before passing to this script, otherwise all files will be downloaded (which is the equivalent of copying the entire share and is bad)

**This script _requires_ SMBList.pl be pipped in to it. Look at "Example Usage" below**
## Links
[Github](https://github.com/Raikia/SMBCrunch)
# Usage
SMB Hunt - Find SMB Null Session
SMB List - Takes output from SMBHunt and perform a recursive directory listing of those shares using the credentials provided
SMB Grab - Grabs files from shares

SMBHunt - After finding what hosts have 445 open with Nmap:
```
./SMBHunt.pl -i ../working/445.txt
```
View shares:
```
smbclient -N //host/share
```