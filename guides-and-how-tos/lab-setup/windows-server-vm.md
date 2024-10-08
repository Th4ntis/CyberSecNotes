# Windows Server VM

I usually go with a [Windows Server 2019](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019) VM with [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/). I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

## Windows Server 2019

Start with our Typical Configuration

![](<../../.gitbook/assets/image (247).png>)

Install the Operating System Later

![](<../../.gitbook/assets/image (422).png>)

Choose Windows and i'll be doing Server 2019 but you can go with whatever edition you're installing

![](<../../.gitbook/assets/image (248).png>)

Choose the path for it and the Name of the VM

![](<../../.gitbook/assets/image (586).png>)

Select the size of the VM. This will **NOT** the overall size, this is just the max size of the VMs HDD space and will fill up as we add more to the VM that takes up space.

If this VM will be on a PC and not be used from an external HDD or moved around you can store it as a single file but if you plan on using this VM on other PC or from an external HDD it's a better idea to split it into multiple files.

Depending on your space, you can edit how much you want. I usually go with the default personally.

![](<../../.gitbook/assets/image (425).png>)

Finally we can now customize our hardware. This is where we can customize the RAM, Processors, ISO files, Network Settings, etc. This is where we select our Windows Server ISO.

I usually increase the RAM for the install so it goes quicker then drop it down after.

![](<../../.gitbook/assets/image (636).png>)

Start our VM and be ready to push a button to boot to the ISO as the screen will say. This is a pretty standard install, mostly just clicking next.

![](<../../.gitbook/assets/image (757).png>)

![](<../../.gitbook/assets/image (786).png>)

Choose the "Windows Server 20XX Standard Evaluation (Desktop Experience)"

![](<../../.gitbook/assets/image (557).png>)

![](<../../.gitbook/assets/image (720).png>)

Go Custom Install

![](<../../.gitbook/assets/image (623).png>)

Click Next

![](<../../.gitbook/assets/image (701).png>)

Let it install

![](<../../.gitbook/assets/image (677).png>)

After install is done, the VM should reboot and bring you to a screen to set your Admin password.

![](<../../.gitbook/assets/image (577).png>)

After that you should be good to log in!

![](<../../.gitbook/assets/image (762).png>)

Now we install VMWare tools with VM > Tools > Install VMWare Tools

Now we can open File Explorer and go to "This PC" to run the Installer.

![](<../../.gitbook/assets/image (775).png>)

This is a typical install, just click next through it all. This will ask to restart the PC, but don't do that yet, we will have to restart anyway in the next parts of the setup.

Now is when you will want to shut down the VM and adjust RAM and Processors if needed. Drop it for 2GB or 4GB of RAM and 1 or 2 processors.

![](<../../.gitbook/assets/image (355).png>)

I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.

Now I am going to take this tip from John Hammond. After you create the Snap Shot, I recommend going into the VMS options, changing the name to Some form of Template and Options and enabling Template mode. So clone the VM choosing the Snapshot when we want to make a VM using this one so we don't have to re-create the VM from scratch every time.

![](<../../.gitbook/assets/image (706).png>)

### Domain Controller Setup

We have our Server Dashboard open

![](<../../.gitbook/assets/image (174).png>)

To set this up for our domain controller, in top right: Manage > Add Roles and Features

Most of this will be standard of clicking next

![](<../../.gitbook/assets/image (528).png>)

Role-based or feature-based Installation

![](<../../.gitbook/assets/image (648).png>)

![](<../../.gitbook/assets/image (764).png>)

Now is where we select "Active Directory Domain Services", with the popup, Select Add Features, then click next.

![](<../../.gitbook/assets/image (681).png>)

![](<../../.gitbook/assets/image (163).png>)

From here it'll be "Next" till the end

![](<../../.gitbook/assets/image (455).png>)

![](<../../.gitbook/assets/image (569).png>)

![](<../../.gitbook/assets/image (316).png>)

Click Install and let it install

![](<../../.gitbook/assets/image (149).png>)

Installed!

![](<../../.gitbook/assets/image (722).png>)

Now we should name our Domain Controller. Start Menu > Search for "Rename"

![](<../../.gitbook/assets/image (224).png>)

Click "Rename this PC"

![](<../../.gitbook/assets/image (692).png>)

Rename it to what you see fit

![](<../../.gitbook/assets/image (356).png>)

Restart the VM

Our Dashboard is showing us a "Warning" Dialog

![](<../../.gitbook/assets/image (191).png>)

![](<../../.gitbook/assets/image (199).png>)

Click Promote this server to a domain controller

We're going to add a new Forest and give it a name

![](<../../.gitbook/assets/image (349).png>)

Give the DSRM a password. I set it the same as the Admin password. (Not the most secure, but this is for a lab environment)

![](<../../.gitbook/assets/image (211).png>)

Then from here it'll be standard Next to Install

![](<../../.gitbook/assets/image (566).png>)

This screen may take a min to finish loading

![](<../../.gitbook/assets/image (378).png>)

![](<../../.gitbook/assets/image (389).png>)

![](<../../.gitbook/assets/image (200).png>)

Now we install it

![](<../../.gitbook/assets/image (336).png>)

![](<../../.gitbook/assets/image (439).png>)

Once done will automatically reboot. After reboot and login, we should now see

![](<../../.gitbook/assets/image (530).png>)

After we Setup user machine and connect them to the Domain, we will do more.

### Post Setup Setup

Now that we have the basics out of the way, lets add some users, groups, and policies.

From the Server Manager Dashboard > Tools (Top Right) > Active Directory Users and Computers

![](<../../.gitbook/assets/image (177).png>)

![](<../../.gitbook/assets/image (197).png>)

I'm going to make a separate Organizational Unit (OU) for Groups just for organization.

Right Click on the Domain.local > New > Organizational Unit

![](<../../.gitbook/assets/image (619).png>)

![](<../../.gitbook/assets/image (469).png>)

Then Select all the Groups and Drag them into the Groups Folder, so there should only be Administrator and Guest in the Users folder and all the groups in the Groups folder. Easy.

![](<../../.gitbook/assets/image (512).png>)

So let's add our Users. Right click in a blank area in Users > New > User

![](<../../.gitbook/assets/image (457).png>)

![](<../../.gitbook/assets/image (154).png>)

Add some users and choose the naming convention. For my example my user doesn't have a last name but if you choose to and want to have a naming convention of first.last or FLast or FirstL, this is where you do that.&#x20;

![Example 1](<../../.gitbook/assets/image (537).png>)

![User with First and Last name](<../../.gitbook/assets/image (380).png>)

Give the user a password, uncheck making the user change the password, and set the password to never expire. This is a VERY bad practice but for a lab environment things will setup a little different than in the real world, at least we hope.

![](<../../.gitbook/assets/image (448).png>)

![](<../../.gitbook/assets/image (606).png>)

Make another user BUT instead of creating it, right click on Administrator, copy it, and follow the same procedure. This will create a second Domain Admin account.

Create a second base normal user as well.

Now we're also going to setup a file share. From the Server Manager Dashboard > File and Storage Services (Left Hand Side) > Shares

![](<../../.gitbook/assets/image (431).png>)

![](<../../.gitbook/assets/image (747).png>)

From the top click on Tasks drop down and select new share > SMB Share - Quick > Next

![](<../../.gitbook/assets/image (609).png>)

![](<../../.gitbook/assets/image (333).png>)

Give the share a name

![](<../../.gitbook/assets/image (719).png>)

Then just click next till it asks you to create it, create the share.

![](<../../.gitbook/assets/image (264).png>)

![](<../../.gitbook/assets/image (308).png>)

Now we are done!

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

***

## Windows Server 2022

Starting with typical setup

![](<../../.gitbook/assets/image (498).png>)

Install the Operating System later

![](<../../.gitbook/assets/image (406).png>)

Choose Windows Server 2019 as the the closest we can get at the current moment.

![](<../../.gitbook/assets/image (407).png>)

Choose the path for it and the Name of the VM

![](<../../.gitbook/assets/image (515).png>)

Select the size of the VM. This will **NOT** the overall size, this is just the max size of the VMs HDD space and will fill up as we add more to the VM that takes up space.

If this VM will be on a PC and not be used from an external HDD or moved around you can store it as a single file but if you plan on using this VM on other PC or from an external HDD it's a better idea to split it into multiple files.

Depending on your space, you can edit how much you want. I usually go with the default personally.

![](<../../.gitbook/assets/image (175).png>)

Finally we can now customize our hardware. This is where we can customize the RAM, Processors, ISO files, Network Settings, etc. This is where we select our Windows Server ISO.

I usually increase the RAM for the install so it goes quicker then drop it down after.

![](<../../.gitbook/assets/image (594).png>)

Start our VM and be ready to push a button to boot to the ISO as the screen will say. This is a pretty standard install, mostly just clicking next.

Once we get to this screen, we have some options. Typical it's with or without Desktop experience. I'm use to Desktop Experience with 2019 and previous, so i'm going to switch it up this time go with  out the Desktop experience so it's just CLI(Command Line Interface).

![](<../../.gitbook/assets/image (500).png>)

Hit he checkbox to agree to terms, and next

![](<../../.gitbook/assets/image (740).png>)

Custom

![](<../../.gitbook/assets/image (209).png>)

Select the drive and click next and let it install, it will automatically reboot.

Once it reboots, follow the prompts, set your admin password. and you'll be brought to the SConfig menu.

![](<../../.gitbook/assets/image (332).png>)

I would start by going to 6, then 1 to update everything

![](<../../.gitbook/assets/image (274).png>)

Once updated are complete and a reboot is done, I recommend installing VMWare tools. First we need to shutdown the VM and remove the ISO file. Edit the VM Settings. I'm choosing physical drive simply because my machine does not have a CD Drive.

![](<../../.gitbook/assets/image (705).png>)

After you've powered back on the machine, from the VMWare menu > VM > Install VMWareTools. Then from the SConfig, type 15 to go to the powershell menu, go to the D: Drive and running setup64.exe

![](<../../.gitbook/assets/image (320).png>)

![](<../../.gitbook/assets/image (652).png>)

We may need to move the window to see the VMWare Tools window.

![](<../../.gitbook/assets/image (395).png>)

After this install and reboots, we can shut it down.

Now is when you will want to shut down the VM and adjust RAM and Processors if needed. Drop it for 2GB or 4GB of RAM and 1 or 2 processors.

![](<../../.gitbook/assets/image (355).png>)

I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.

Now I am going to take this tip from John Hammond. After you create the Snap Shot, I recommend going into the VMS options, changing the name to Some form of Template and Options and enabling Template mode. So clone the VM choosing the Snapshot when we want to make a VM using this one so we don't have to re-create the VM from scratch every time.

![](<../../.gitbook/assets/image (706).png>)

### Domain Controller Setup

We should first run `SConfig` to change the hostname and set a static IP.

After this we can run the following command to turn this into a DC.

```
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Import-Module ADDSDeployment
install-ADDSForest
```

![](<../../.gitbook/assets/image (463).png>)

Now once it has been restarted we can add computers to the domain. We can do this via GUI, or command line with

`Add-Computer -DomainName web.local -Credential web\Administrator -Force -Restart` - Changing the web.local and web\Administrator, to what you changed your DomainName to from the previous step.
