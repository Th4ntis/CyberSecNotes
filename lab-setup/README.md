# ⚗️ Lab Setup



## About

We have [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/) for Virual Machine Applications. I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

For Linux VMs I use [Kubuntu](https://kubuntu.org/) usually just as I prefer KDE. We can go with a [Kali Linux VM](https://www.kali.org/get-kali/) but with this we get to learn about installing specific tools from source, compiling them, and can have just the tools we want/use.&#x20;

I typically test on/against [Windows 10 Enterprise](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise) and [Windows Server 2019](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019). There are other evaluation ISOs found [here](https://www.microsoft.com/en-us/evalcenter/) on Microsoft website, such as Windows 11 and Windows Server 2022.

| Attack                 | Defense                                |
| ---------------------- | -------------------------------------- |
| [Ubuntu](ubuntu-vm.md) | [Windows](windows-user-vm.md)          |
| [Kali](kali-vm.md)     | [Windows Server](windows-server-vm.md) |

## Creating Snapshots

### VMWare

This feature is unfortunately only available on Workstation Pro. If you have VMWare Player, you can created a copy of the folder, this does however use more Disk Space.

If you have Workstation Pro, with the VM selected, from the menu bar: `VM > Snapshot > Take Snapshot...` from here we can name the snapshot and give it a description.

### Virtualbox

`Right click on the VM(Or click the settings menu icon for the VM) > Snapshots` from here we can creature the snapshot, name it, and give it a description

## Restoring Snapshots

### VMWare

This feature is unfortunately only available on Workstation Pro. If you have VMWare Player, you can use the copy of the folder you created, just make sure you remove the old folder and make a new one so you always have a backup.

If you have Workstation Pro, with the VM selected, from the menu bar: `VM > Snapshot > Revert to Snapshot`

### Virtualbox

`Right click on the VM (or click the settings menu icon for the VM) > Snapshots` from here we can creature the snapshot, name it, and give it a description
