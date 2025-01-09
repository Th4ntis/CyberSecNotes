# Windows User VM

I usually go with a [Windows 11](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise) VM with [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/). I have VMWare Workstation Pro as Broadcom bought out VMWare and made it free, you just need an account with them. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

## VMWare Setup

Starting with typical setup

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FsnQye1BjFW53yx8blAvF%252Fimage.png%3Falt%3Dmedia%26token%3D2b443419-09d7-4e80-b3fe-69c62291eb01&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ebd1da4a&#x26;sv=2" alt=""><figcaption></figcaption></figure>

I add the .iso after

<figure><img src="../../.gitbook/assets/image (1).avif" alt=""><figcaption></figcaption></figure>



Select the size of the VM. This will **NOT** the overall size, this is just the max size of the VMs HDD space and will fill up as we add more to the VM that takes up space.

If this VM will be on a PC and not be used from an external HDD or moved around you can store it as a single file but if you plan on using this VM on other PC or from an external HDD it's a better idea to split it into multiple files.

<figure><img src="../../.gitbook/assets/image (3).avif" alt=""><figcaption></figcaption></figure>

Finally we can now customize our hardware. This is where we can customize the RAM, Processors, ISO files, Network Settings, etc. This is where we select our Windows Server ISO.

I recommend disabling the Printer, Sound Card, and under Display unchecking 'Accelerate 3D Graphics'.

I usually increase the RAM for the install so it goes quicker then drop it down after.

For install purposes, I up it to 8GB of ram and 4 Processors. Also add in the .iso file now.

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252F5Uqo0wIHz0nrjvfdV9EZ%252Fimage.png%3Falt%3Dmedia%26token%3Dd79f9af0-7219-4f27-a44b-a2a79d8845ca&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=6b4fe7f6&#x26;sv=2" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4).avif" alt=""><figcaption></figcaption></figure>



When finished, click close > finish > turn on the VM. Be sure to click into the VM to press a button when it starts.

## Installing Windows 11

<figure><img src="../../.gitbook/assets/image (5).avif" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6).avif" alt=""><figcaption></figcaption></figure>

You MAY need to bypass TPM. If so, continue on. If not, skip ahead a little bit to [INSTALL NOW](windows-user-vm.md#install-now).

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

### Install Now

Click INSTALL NOW, then accept the EULA and click next

<figure><img src="../../.gitbook/assets/image (7).avif" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).avif" alt=""><figcaption></figcaption></figure>

I go with the custom installation option.

<figure><img src="https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FqbLVgMtuGMWVbf0sbv7J%252Fimage.png%3Falt%3Dmedia%26token%3D831bd2a6-fec9-4cb3-92b6-4ce38873096e&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=c15f4953&#x26;sv=2" alt=""><figcaption></figcaption></figure>

Select the hard drive and click next

Click Next

<figure><img src="../../.gitbook/assets/image (9).avif" alt=""><figcaption></figcaption></figure>

Wait for the install process to finish and restart

<figure><img src="../../.gitbook/assets/image (10).avif" alt=""><figcaption></figcaption></figure>

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

### Joining a domain

We need to set out DNS Server to be the IP of our Domain Controller. So open the start menu, search for and open Control Panel.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

In the top right, change it from 'Category' to 'Small/Large Icons', then open network and sharing center.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

On the left hand side, select 'Change Adapter Settings', then right click on the adapter, and select properties.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Select Internet Protocol Version 4 (TCP/IPv4) and then properties.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Change the DNS settings and set it to be the Domain Controllers IP address.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Open the start menu and search for domain, and select 'Access work or school'

![](<../../.gitbook/assets/image (359).png>)

Click the blue 'Connect' button

![](<../../.gitbook/assets/image (546).png>)

Select 'Join this device to a local Active Directory domain'.

![](<../../.gitbook/assets/image (198).png>)

and follow the steps. Add in your domain name followed by .local, Eg. Gibson.local, sign in with Domain Admin credentials, reboot, and ta-da!
