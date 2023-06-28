# Windows User VM

I usually go with a [Windows 10](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise) VM with [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/). I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

## Starting

We will as before, do a Typical install

![](<../../../.gitbook/assets/image (273).png>)

Install the System later

![](<../../../.gitbook/assets/image (263).png>)

Select the Windows OS.

![](<../../../.gitbook/assets/image (232).png>)

Select a path and name the VM. For this I will be naming the VM after the User that I plan on using on this VM.

![](<../../../.gitbook/assets/image (244).png>)

Select the size of the VM. This will **NOT** the overall size, this is just the max size of the VMs HDD space and will fill up as we add more to the VM that takes up space.

If this VM will be on a PC and not be used from an external HDD or moved around you can store it as a single file but if you plan on using this VM on other PC or from an external HDD it's a better idea to split it into multiple files.

Depending on your space, you can edit how much you want. I usually go the default 60GB.

![](<../../../.gitbook/assets/image (245).png>)

Finally we can now customize our hardware. This is where we can customize the RAM, Processors, ISO files, Network Settings, etc. This is where we select our Windows Server ISO.

I recommend disabling the Printer, Sound Card, and under Display unchecking 'Accelerate 3D Graphics'.

I usually increase the RAM for the install so it goes quicker then drop it down after.

![](<../../../.gitbook/assets/image (214).png>)

## Windows 10

Start the VM and press any button to boot from the ISO.

![](<../../../.gitbook/assets/image (241).png>)

Click INSTALL NOW, then accept the EULA and click next

![](<../../../.gitbook/assets/image (198).png>)

Custom Install

![](<../../../.gitbook/assets/image (275).png>)

Click Next

![](<../../../.gitbook/assets/image (278).png>)

Let it install

![](<../../../.gitbook/assets/image (209).png>)

After install and it reboots

![](<../../../.gitbook/assets/image (284).png>)

![](<../../../.gitbook/assets/image (249).png>)

Skip adding a second layout, unless you would like one

Click Domain Join instead when asked to Sign Into Microsoft

![](<../../../.gitbook/assets/image (204).png>)

Enter the Username and Password. I recommend a basic password (Eg. Password1, Password 123, etc.) for the user(s) since this for testing purposes. Then for Security Questions, you can put whatever you want, I wouldn't use real world info as this is for a lab.

![](<../../../.gitbook/assets/image (225).png>)

Turn off all settings

![](<../../../.gitbook/assets/image (205).png>)

Choose Not Now

![](<../../../.gitbook/assets/image (265).png>)

Let the install finish with post setup stuff

![](<../../../.gitbook/assets/image (228).png>)

Now we have our desktop. Time to do some basic setup.

![](<../../../.gitbook/assets/image (219).png>)

Install VMWare Tools, and Rename the PC, then Add it to the Domain if you are going that route.

In the Menu Bar of VMWare > VM > Install VMWare Tools

Inside the VM open File Explorer > This PC > Run the VMWare Tools installer

![](<../../../.gitbook/assets/image (289).png>)

Then a basic click next on everything. Don't reboot when done since you'll want to reboot after you rename the PC as well.

Open Start Menu, type in Rename

![](<../../../.gitbook/assets/image (287).png>)

Rename this PC

![](<../../../.gitbook/assets/image (283).png>)

![](<../../../.gitbook/assets/image (210).png>)

Reboot to apply changes and you're done! BUT if you want to add it to a domain, we continue on.

Now is when you will want to shut down the VM and adjust RAM and Processors if needed. Drop it for 2GB or 4GB of RAM and 1 or 2 processors.

![](<../../../.gitbook/assets/image (216).png>)

### Joining a Domain

You _may_ want a second user machine as well but only if you're machine is capable of it. It's not required but it will help.

![](<../../../.gitbook/assets/image (216).png>)

This process will be the same for both machines if setting up two.

First we need to get the IP of our Domain Controller. Command Prompt > `ipconfig`

![](<../../../.gitbook/assets/image (292).png>)

We need to set the users machine DNS to our Domain Controllers IP.

On the Users machine: Start Menu > Setting Icon > Network & Internet > Change Adapter Options

![](<../../../.gitbook/assets/image (224).png>)

![](<../../../.gitbook/assets/image (256).png>)

Right click on the Ethernet Adapter > Properties > Double Click on Internet Protocol Version 4 (TCP/IPv4)

![](<../../../.gitbook/assets/image (261).png>)

Change the DNS option to your Domain Controllers IP > OK

![](<../../../.gitbook/assets/image (207).png>)

From here on the Users machine still: Star Menu > Domain > Access Work or School

![](<../../../.gitbook/assets/image (206).png>)

![](<../../../.gitbook/assets/image (220).png>)

Click connect then at the bottom of the window select "Join a local Active Directory Domain"

![](<../../../.gitbook/assets/image (262).png>)

It'll ask for the domain name

![](<../../../.gitbook/assets/image (295).png>)

Then should ask who do you want to join as. At first join as Admin.

![](<../../../.gitbook/assets/image (234).png>)

Skip this step

![](<../../../.gitbook/assets/image (277).png>)

Then Reboot. Once it's rebooted and at the login screen, select "Other User" In the bottom left.

![](<../../../.gitbook/assets/image (268).png>)

Input the username and password of a user you created

![](<../../../.gitbook/assets/image (208).png>)

After you have signed in with a user you created. Sing out and sign back in as the Administrator. You will need to add the domain before the Administrator name or it will try to log you in as the local admin.

![](<../../../.gitbook/assets/image (221).png>)

We're going to add the user we logged in as, as an admin on this computer. Start Menu > Computer Management > Local Users and Groups > Groups > Administrators

![](<../../../.gitbook/assets/image (203).png>)

![](<../../../.gitbook/assets/image (202).png>)

Double Click on Administrators > Add > Type in user name > Check Names > Ok

![](<../../../.gitbook/assets/image (252).png>)

Apply > Ok

![](<../../../.gitbook/assets/image (239).png>)

All set! We now have a lab Environment with Ubuntu for an attack machine if needed, a Windows Domain Controller/Server and a User or Two. We can now install whatever tools or software we may want onto them.

I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.

## Windows 11

Same way as Windows 10 but once met with this screen

![](<../../../.gitbook/assets/image (281).png>)

Press `Shift+F10` to bring up the Command Prompt

![](<../../../.gitbook/assets/image (282).png>)

Run `regedit` and navigate to `HKEY_`_`LOCAL_MACHINE\SYSTEM\Setup` and make a new Key called "LabConfig"_

![](<../../../.gitbook/assets/image (250).png>)

_Inside there create DWord(32-Bit) Values for:_

* _BypassTPMCheck_
* _BypassRAMCheck_
* _BypassSecureBootCheck_

_and change their value to 1_

![](<../../../.gitbook/assets/image (260).png>)

Close out that window to exit the installation and start from the beginning window.

Click INSTALL NOW, then accept the EULA and click next

![](<../../../.gitbook/assets/image (198).png>)

Custom Install

![](<../../../.gitbook/assets/image (275).png>)

Click Next

![](<../../../.gitbook/assets/image (278).png>)

Let it install

![](<../../../.gitbook/assets/image (209).png>)

After install and it reboots

![](<../../../.gitbook/assets/image (296).png>)

We choose our region, keyboard layout, etc. and we can setup our account. Select 'sign-in options'

![](<../../../.gitbook/assets/image (311).png>)

Then 'Domain Join Instead'

![](<../../../.gitbook/assets/image (309).png>)

Input our username and password, password confirmation, and security questions

![](<../../../.gitbook/assets/image (313) (1).png>)

Disable all the privacy settings and click accept.

![](<../../../.gitbook/assets/image (318).png>)

It will now do Windows setup and such

![](<../../../.gitbook/assets/image (316).png>)

We're now logged in and can install VMWare Tools

![](<../../../.gitbook/assets/image (302).png>)

![](<../../../.gitbook/assets/image (320).png>)

### Joining a domain

Same way we would for Windows 10. Open the start menu and search for domain, and select 'Access work or school'

![](<../../../.gitbook/assets/image (317).png>)

Click the blue 'Connect' button

![](<../../../.gitbook/assets/image (315).png>)

Select 'Join this device to a local Active Directory domain'.

![](<../../../.gitbook/assets/image (301).png>)

&#x20;and follow the steps. Add in your domain name, sign in with Admin credentials, reboot, and ta-da!
