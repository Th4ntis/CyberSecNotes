# Windows User VM

I usually go with a [Windows 11](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise) VM with [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/). I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

## Starting

We will do a Typical install

![](<../../.gitbook/assets/image (520).png>)

Install the System later

![](<../../.gitbook/assets/image (604).png>)

Select the Windows OS.

![](<../../.gitbook/assets/image (287).png>)

Select a path and name the VM. For this I will be naming the VM after the User that I plan on using on this VM.

![](<../../.gitbook/assets/image (253).png>)

Select the size of the VM. This will **NOT** the overall size, this is just the max size of the VMs HDD space and will fill up as we add more to the VM that takes up space.

If this VM will be on a PC and not be used from an external HDD or moved around you can store it as a single file but if you plan on using this VM on other PC or from an external HDD it's a better idea to split it into multiple files.

Depending on your space, you can edit how much you want. I usually go the default 60GB.

![](<../../.gitbook/assets/image (447).png>)

Finally we can now customize our hardware. This is where we can customize the RAM, Processors, ISO files, Network Settings, etc. This is where we select our Windows Server ISO.

I recommend disabling the Printer, Sound Card, and under Display unchecking 'Accelerate 3D Graphics'.

I usually increase the RAM for the install so it goes quicker then drop it down after.

![](<../../.gitbook/assets/image (397).png>)

## Windows 11



![](<../../.gitbook/assets/image (548).png>)

Press `Shift+F10` to bring up the Command Prompt

![](<../../.gitbook/assets/image (712).png>)

Run `regedit` and navigate to `HKEY_`_`LOCAL_MACHINE\SYSTEM\Setup` and make a new Key called "LabConfig"_

![](<../../.gitbook/assets/image (745).png>)

_Inside there create DWord(32-Bit) Values for:_

* _BypassTPMCheck_
* _BypassRAMCheck_
* _BypassSecureBootCheck_

_and change their value to 1_

![](<../../.gitbook/assets/image (713).png>)

Close out that window to exit the installation and start from the beginning window.

Click INSTALL NOW, then accept the EULA and click next

![](<../../.gitbook/assets/image (283).png>)

Custom Install

![](<../../.gitbook/assets/image (541).png>)

Click Next

![](<../../.gitbook/assets/image (315).png>)

Let it install

![](<../../.gitbook/assets/image (426).png>)

After install and it reboots&#x20;

![](<../../.gitbook/assets/image (779).png>)

We choose our region, keyboard layout, etc. and we can setup our account. Select 'sign-in options'

![](<../../.gitbook/assets/image (242).png>)

Then 'Domain Join Instead'

![](<../../.gitbook/assets/image (390).png>)

Input our username and password, password confirmation, and security questions

![](<../../.gitbook/assets/image (462).png>)

Disable all the privacy settings and click accept.

![](<../../.gitbook/assets/image (290).png>)

It will now do Windows setup and such

![](<../../.gitbook/assets/image (768).png>)

We're now logged in and can install VMWare Tools

![](<../../.gitbook/assets/image (346).png>)

![](<../../.gitbook/assets/image (454).png>)

###

***

### Joining a domain

Same way we would for Windows 10. Open the start menu and search for domain, and select 'Access work or school'

![](<../../.gitbook/assets/image (359).png>)

Click the blue 'Connect' button

![](<../../.gitbook/assets/image (546).png>)

Select 'Join this device to a local Active Directory domain'.

![](<../../.gitbook/assets/image (198).png>)

&#x20;and follow the steps. Add in your domain name, sign in with Admin credentials, reboot, and ta-da!
