# Ubuntu VM

I usually go with an [Ubuntu](https://ubuntu.com/) (I usually go with [Kubuntu](https://kubuntu.org/)) VM with [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/). I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

We can go with a [Kali Linux VM](https://www.kali.org/get-kali/) but with this we get to learn about installing specific tools from source, compiling them, and can have just the tools we want/use.&#x20;

## \*buntu

We will start with the Typical configuration

![](<../../.gitbook/assets/image (254).png>)

Then install choose "I will install the Operating System Later"

![](<../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1).png>)

Select Linux, then select the Ubuntu 64-bit version.

![](<../../.gitbook/assets/image (11) (1) (2).png>)

Name it and choose a location to store the VM files

![](<../../.gitbook/assets/image (398).png>)

Select the size of the VM. This will **NOT** the overall size, this is just the max size of the VMs HDD space and will fill up as we add more to the VM that takes up space.

If this VM will be on a PC and not be used from an external HDD or moved around you can store it as a single file but if you plan on using this VM on other PC or from an external HDD it's a better idea to split it into multiple files.

Depending on your space, you can edit how much you want. I usually go 60GB or 80GB depending.

![](<../../.gitbook/assets/image (400).png>)

Finally we can now customize our hardware. This is where we can customize the RAM, Processors, ISO files, Network Settings, etc. This is where we select our Ubuntu ISO.

![](<../../.gitbook/assets/image (273).png>)

![](<../../.gitbook/assets/image (262).png>)

Now we close that and can start our VM and install it. This process will be VERY similar for each desktop environment just may look different. Once we start the VM, itll take us to a list, we can select the first option or just let it auto select it after 10 seconds.

So from here we select "Install \*buntu"

![](<../../.gitbook/assets/image (401).png>)

Select language and keyboard layout

![](<../../.gitbook/assets/image (270).png>)

Make sure you tick 'install third-party software for graphics..." and such.&#x20;

![](<../../.gitbook/assets/image (453).png>)

As this is on a VM, this default option is ok for this.

![](<../../.gitbook/assets/image (9) (3).png>)

![](<../../.gitbook/assets/image (275).png>)

Select Timezone

![](<../../.gitbook/assets/image (19) (1).png>)

Setup the username, hostname, and password

![](<../../.gitbook/assets/image (408).png>)

Let the install finish

![](<../../.gitbook/assets/image (267).png>)

![](<../../.gitbook/assets/image (26) (1) (1).png>)

If it asks you to "Remove the installation media and press ENTER" just press `ENTER`.

![](<../../.gitbook/assets/image (260).png>)

From here it will restart and you will be taken to a login screen. So login and ta-da!

![](<../../.gitbook/assets/image (257).png>)

![](<../../.gitbook/assets/image (12) (1) (1).png>)

Depending which Desktop Environment (DE) you chose, you're may look different but that is ok, it's still the same system under the hood.

Once we're in, it's a good idea to open the terminal, in Kubuntu it's called `Konsole`, and we update everything with `sudo apt update && sudo apt upgrade -y`.

Now is when you will want to shut down the VM and adjust RAM and Processors if needed. Drop it for 2GB or 4GB of RAM and 1 or 2 processors.

![](<../../.gitbook/assets/image (329).png>)

From here you can explore and find things, change settings, and learn. I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.
