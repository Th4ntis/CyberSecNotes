# Windows Server VM

I usually go with a [Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022) VM with [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/). I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

## VMWare Setup

Starting with typical setup

<figure><img src="../../.gitbook/assets/image (1013).png" alt=""><figcaption></figcaption></figure>

I add the .iso after

<figure><img src="../../.gitbook/assets/image (1014).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1015).png" alt=""><figcaption></figcaption></figure>

Name the VM and where it's stored

<figure><img src="../../.gitbook/assets/image (1016).png" alt=""><figcaption></figcaption></figure>

How much space you want the VM to have. Note that this is not how much space it will take up unless it ends up using all 100GB. I also keep mine as a single file as I keep this on one machine rather than multiple.

<figure><img src="../../.gitbook/assets/image (1017).png" alt=""><figcaption></figcaption></figure>

Now we can customize the hardware for it.

<figure><img src="../../.gitbook/assets/image (1018).png" alt=""><figcaption></figcaption></figure>

For install purposes, I up it to 8GB of ram and 4 Processors. Also add in the .iso file now.

<figure><img src="../../.gitbook/assets/image (1019).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1020).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1021).png" alt=""><figcaption></figcaption></figure>

When finished, click close > finish > turn on the VM. Be sure to click into the VM to press a button when it starts.&#x20;

### Installing Windows Server 2022

this section is all just defaults of clicking Next

<figure><img src="../../.gitbook/assets/image (1022).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1023).png" alt=""><figcaption></figcaption></figure>

I select the option with a Desktop Environment.

<figure><img src="../../.gitbook/assets/image (1025).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1026).png" alt=""><figcaption></figcaption></figure>

I go with the custom installation option.

<figure><img src="../../.gitbook/assets/image (1027).png" alt=""><figcaption></figcaption></figure>

Select the hard drive and click next

<figure><img src="../../.gitbook/assets/image (1028).png" alt=""><figcaption></figcaption></figure>

Wait for the install process to finish and restart

<figure><img src="../../.gitbook/assets/image (1029).png" alt=""><figcaption></figcaption></figure>

### Setting up the Server

When it restarts it will ask you for your Administrator password, use whatever you'd like, just remember this is for a lab environment, so it should be something simple/crackable.

<figure><img src="../../.gitbook/assets/image (1030).png" alt=""><figcaption></figcaption></figure>

Log in with the password you just set. Select "Yes" when asked to have the PC discoverable.

<figure><img src="../../.gitbook/assets/image (1031).png" alt=""><figcaption></figcaption></figure>

I usually start with installing VMWare tools and renaming the PC. When it comes to Installing VMWare tools, I do the complete installation and choose "no" to restarting as we will restart after we rename the PC. To rename the PC, open the start menu and type in "rename".

<figure><img src="../../.gitbook/assets/image (1032).png" alt=""><figcaption></figcaption></figure>

Select "Rename this PC" and give it a new name. Remember this is your Domain Controller(DC).

<figure><img src="../../.gitbook/assets/image (1033).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1034).png" alt=""><figcaption></figcaption></figure>

It will prompt you to restart your PC. Restart it, log back in and we will turn this into our DC. With the Server Manager open, click manage in the top right and select "Add Roles and Features".

<figure><img src="../../.gitbook/assets/image (1035).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1036).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1037).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1038).png" alt=""><figcaption></figcaption></figure>

From here, select "Active Directory Domain Services". Then click "Add Features".

<figure><img src="../../.gitbook/assets/image (1040).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1039).png" alt=""><figcaption></figcaption></figure>

Now click "Next" until the end, then click "Install". Once it installs, select close, and we promote it to a DC. In the Server manager, in the top right, it will be a flag with a yellow exclamation mark. Select it, then click where it says "Promote the server to a domain controller".

<figure><img src="../../.gitbook/assets/image (1041).png" alt=""><figcaption></figcaption></figure>

Add a new forest and give it a name, be sure to add ".local" to the end of it.

<figure><img src="../../.gitbook/assets/image (1042).png" alt=""><figcaption></figcaption></figure>

It will ask for a password, I give it the same password as the Administrator user. This is not a secure practice, but this is for our lab environment.

<figure><img src="../../.gitbook/assets/image (1043).png" alt=""><figcaption></figcaption></figure>

From here, click "next" until we can install it and it will restart the machine. Once it restarts, the login screen will show the domain name\user account, indicating your logging into the domain with the user.

<figure><img src="../../.gitbook/assets/image (1044).png" alt=""><figcaption></figcaption></figure>

Now lets add another feature, Active Directory Certificate Services. We go through the same process as adding the last feature till we can select it.

<figure><img src="../../.gitbook/assets/image (1045).png" alt=""><figcaption></figcaption></figure>

From here, it will again be, next till we can install it. Once installed, we will have another notification by the flag in the server manager.

<figure><img src="../../.gitbook/assets/image (1046).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1047).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1048).png" alt=""><figcaption></figcaption></figure>

It will be another simple, next till the end from here. Select Configure in the bottom right, and we're set!

<figure><img src="../../.gitbook/assets/image (1049).png" alt=""><figcaption></figcaption></figure>

### Adding users

Now lets add some users to our Domain. Make a .csv file with firstname, lastname, username, password, and ou.

<figure><img src="../../.gitbook/assets/image (1050).png" alt=""><figcaption></figcaption></figure>

Copy that to the server and open it with notepad.

<figure><img src="../../.gitbook/assets/image (1051).png" alt=""><figcaption></figcaption></figure>

Now open Powershell ISE, make a new file paste in the following code, editing your DC name.

```powershell
Import-Module activedirectory

#Point to csv file containing users!
$UserFile = Import-csv C:\Users\Administrator\Desktop\users.csv

#Change this to your domain
$Domain = 'GIBSON.local'

foreach ($User in $UserFile)
{
        
    $Username 	= $User.username
    $Password 	= $User.password
    $Firstname 	= $User.firstname
    $Lastname 	= $User.lastname
    $OU 		= $User.ou

    #Check user does not exist
    if (Get-ADUser -F {SamAccountName -eq $Username})
    {
         #If user exists...
         Write-Warning "Error! $Username already exists."
    }
    else
    {
        #Otherwise...	
        New-ADUser `
            -SamAccountName $Username `
            -UserPrincipalName "$Username@$Domain" `
            -Name "$Firstname $Lastname" `
            -GivenName $Firstname `
            -Surname $Lastname `
            -Enabled $True `
            -DisplayName "$Lastname, $Firstname" `
            -Path $OU `
            -AccountPassword (convertto-securestring $Password -AsPlainText -Force) -ChangePasswordAtLogon $False -PasswordNeverExpires $True
            
    }
}
```

<figure><img src="../../.gitbook/assets/image (1052).png" alt=""><figcaption></figcaption></figure>

Click the green button in the top bar.

<figure><img src="../../.gitbook/assets/image (1053).png" alt=""><figcaption></figcaption></figure>

Now in the server manager, select Tools > Active Directory Users and Computers.

<figure><img src="../../.gitbook/assets/image (1054).png" alt=""><figcaption></figcaption></figure>

Going to 'Users' we should see our list of users.&#x20;

<figure><img src="../../.gitbook/assets/image (1055).png" alt=""><figcaption></figcaption></figure>

But we should also add a service account. So in the users and computers area, right click on a blank spot and select \`Add User\`.

<figure><img src="../../.gitbook/assets/image (1056).png" alt=""><figcaption></figcaption></figure>

Name it SQL-SVC and give it a weak/crackable password, like `P4ssw0rd123!`. Then in an Admin command prompt run the following, ensuring that you choose an arbitrarily large port, not a common one. This will change the account to a service account by assigning it an SPN.

```
setspn -a GIBSON/SQL-SVC.GIBSON.local:55555 GIBSON\SQL-SVC
```

<figure><img src="../../.gitbook/assets/image (1057).png" alt=""><figcaption></figcaption></figure>

Now also, give the SQL-SVC user a description by right clicking on it, and selecting properties.

<figure><img src="../../.gitbook/assets/image (1058).png" alt=""><figcaption></figcaption></figure>

Now is when you will want to shut down the VM and adjust RAM and Processors if needed. Drop it for 2GB or 4GB of RAM and 1 or 2 processors.

![](<../../.gitbook/assets/image (355).png>)

I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.

Now I am going to take this tip from John Hammond. After you create the Snap Shot, I recommend going into the VMS options, changing the name to Some form of Template and Options and enabling Template mode. So clone the VM choosing the Snapshot when we want to make a VM using this one so we don't have to re-create the VM from scratch every time.

![](<../../.gitbook/assets/image (706).png>)

### Optional: Disable Windows Defender

IF you want the other VMs that will join this Domain to have Windows Defender disabled, I recommend doing this for simplicity sake, IF you are pentesting against this and having another VM setup with Defender Enabled to test things against that.

Start Menu > Group Policy > Right Click and Run as Admin

![](<../../.gitbook/assets/image (766).png>)

![](<../../.gitbook/assets/image (613).png>)

Right click on out domain and Create a new Group Policy in this domain (Top option).

![](<../../.gitbook/assets/image (665).png>)

Name this "Disable Windows Defender"

![](<../../.gitbook/assets/image (309).png>)

Right click on newly added "Disable Windows Defender" GPO on the left and Edit it

![](<../../.gitbook/assets/image (231).png>)

Drill Down: Computer Configuration > Policies > Administrative Templates > Windows Components > Windows Defender Antivirus

![](<../../.gitbook/assets/image (382).png>)

![](<../../.gitbook/assets/image (470).png>)

Double click on the "Turn off Windows Defender Antivirus" > Enabled > Apply > Ok

![](<../../.gitbook/assets/image (266).png>)

Close out of the Group Policy Management Editor and on the Group Policy Management Window, with the Disable Windows Defender selected, if 'Enforced' says no, right click on it, and enforce it

![](<../../.gitbook/assets/image (679).png>)

Now we are done!

Again, I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.

##
