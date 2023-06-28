# Kali VM

I typically prefer to install it myself([using the ISO](https://www.kali.org/get-kali/#kali-installer-images)), BUT you can grab a [pre-made VM](https://www.kali.org/get-kali/#kali-virtual-machines) from them. I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

## Kali ISO

We will start with the Typical configuration

<figure><img src="../../../.gitbook/assets/image (300).png" alt=""><figcaption></figcaption></figure>

Then install choose "I will install the Operating System Later"

<figure><img src="../../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

Select Linux, then select the Debian 64-bit version.

<figure><img src="../../../.gitbook/assets/image (440).png" alt=""><figcaption></figcaption></figure>

Give the machine a name and choose where to save it

<figure><img src="../../../.gitbook/assets/image (7) (5).png" alt=""><figcaption></figcaption></figure>

Select the size of the VM. This will **NOT** the overall size, this is just the max size of the VMs HDD space and will fill up as we add more to the VM that takes up space.

If this VM will be on a PC and not be used from an external HDD or moved around you can store it as a single file but if you plan on using this VM on other PC or from an external HDD it's a better idea to split it into multiple files.

Depending on your space, you can edit how much you want. I usually go 60GB or 80GB depending.

<figure><img src="../../../.gitbook/assets/image (438).png" alt=""><figcaption></figcaption></figure>

Finally we can now customize our hardware. This is where we can customize the RAM, Processors, ISO files, Network Settings, etc. This is where we select our Ubuntu ISO.

<figure><img src="../../../.gitbook/assets/image (437).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (441).png" alt=""><figcaption></figcaption></figure>

Now we close that and can start our VM and install it. Once we start the VM, it'll take us to a list, I'm going to choose Graphical Install

<figure><img src="../../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

Choose your language and Region

<figure><img src="../../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (429).png" alt=""><figcaption></figcaption></figure>

Choose your Keyboard layout

<figure><img src="../../../.gitbook/assets/image (110) (1).png" alt=""><figcaption></figcaption></figure>

Give the machine a hostname

<figure><img src="../../../.gitbook/assets/image (439).png" alt=""><figcaption></figcaption></figure>

If you have a domain name you would like this to utilize, input it here. I will be leaving mine blank.

<figure><img src="../../../.gitbook/assets/image (436).png" alt=""><figcaption></figcaption></figure>

Choose a username for your account

<figure><img src="../../../.gitbook/assets/image (433) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (321).png" alt=""><figcaption></figcaption></figure>

Input a password for the user

<figure><img src="../../../.gitbook/assets/image (432).png" alt=""><figcaption></figcaption></figure>

Choose the timezone for the VM

<figure><img src="../../../.gitbook/assets/image (431) (1).png" alt=""><figcaption></figcaption></figure>

For a Vm, we will use the entire disk.

<figure><img src="../../../.gitbook/assets/image (434).png" alt=""><figcaption></figcaption></figure>

Pick the disk you would like to use

<figure><img src="../../../.gitbook/assets/image (442).png" alt=""><figcaption></figcaption></figure>

Pick how you may want to partition the drive. Usually for a VM instance, you can put everything into one partition.

<figure><img src="../../../.gitbook/assets/image (430) (1).png" alt=""><figcaption></figcaption></figure>

Verify the partition changes

<figure><img src="../../../.gitbook/assets/image (312).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (296).png" alt=""><figcaption></figcaption></figure>

Let the VM Install

<figure><img src="../../../.gitbook/assets/image (435).png" alt=""><figcaption></figcaption></figure>

Choose if you want another Desktop Environment(DE) or if you do/don't any extra tools to bein installed

<figure><img src="../../../.gitbook/assets/image (443).png" alt=""><figcaption></figcaption></figure>

After that finishes installing, choose to install the GRUB bootloader

<figure><img src="../../../.gitbook/assets/image (308).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (319).png" alt=""><figcaption></figcaption></figure>

Once install is finished, you'll beboot the system and done!

<figure><img src="../../../.gitbook/assets/image (316).png" alt=""><figcaption></figcaption></figure>

### Post Install

Once we're in, it's a good idea to open the terminal, and we update everything with `sudo apt update && sudo apt upgrade -y`.

Now is when you will want to shut down the VM and adjust RAM and Processors if needed. Drop it for 2GB or 4GB of RAM and 1 or 2 processors.

From here you can explore and find things, change settings, and learn. I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.

I recommend using some additional software such as [PimpMyKali from DeWalt](https://github.com/Dewalt-arch/pimpmykali/blob/master/README.md).

## Kali VM

### VMWare

<figure><img src="../../../.gitbook/assets/image (5) (2) (2).png" alt=""><figcaption></figcaption></figure>

Download the .7z file and extract it with [7Zip](https://www.7-zip.org/) in whatever manor that works for you.

<figure><img src="../../../.gitbook/assets/image (2) (6).png" alt=""><figcaption></figcaption></figure>

With the VM extracted, within VMWare, File > Open, then navigate to the directory with the .vmx file.

<figure><img src="../../../.gitbook/assets/image (5) (2).png" alt=""><figcaption></figcaption></figure>

From here, you can see the default settings on the site, but can edit them better suited to your machine.

<figure><img src="../../../.gitbook/assets/image (444).png" alt=""><figcaption></figcaption></figure>

Upon launching, the default credentials are be the word `kali` for the username AND password.

### Virtualbox

<figure><img src="../../../.gitbook/assets/image (431).png" alt=""><figcaption></figcaption></figure>

Download the .7z file in the and extract it with [7Zip](https://www.7-zip.org/) in whatever manor that works for you.

<figure><img src="../../../.gitbook/assets/image (5) (3).png" alt=""><figcaption></figcaption></figure>

With the VM extracted, select the add button, then navigate to the directory with the .vbox file.

<figure><img src="../../../.gitbook/assets/image (430).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

From here, you can see the default settings on the site, but can edit them better suited to your machine.

<figure><img src="../../../.gitbook/assets/image (433).png" alt=""><figcaption></figcaption></figure>

Upon launching, the default credentials are be the word `kali` for the username AND password.

### Post Install

Once we're in, it's a good idea to open the terminal, and we update everything with `sudo apt update && sudo apt upgrade -y`.

Now is when you will want to shut down the VM and adjust RAM and Processors if needed. Drop it for 2GB or 4GB of RAM and 1 or 2 processors.

From here you can explore and find things, change settings, and learn. I **HIGHLY** recommend creating a snapshot after you have this done and setup so that way you can always revert back to that snapshot if needed if something breaks or you just need to clean things up.

I recommend using some additional software such as [PimpMyKali from DeWalt](https://github.com/Dewalt-arch/pimpmykali/blob/master/README.md).
