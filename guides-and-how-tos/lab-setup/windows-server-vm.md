# Windows Server VM

I usually go with a [Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022) VM with [VMWare](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW\&productId=1039\&rPId=85399) or [Virtualbox](https://www.virtualbox.org/). I have VMWare Workstation Pro but Player works just as well. You can go with either VMWare or Virtualbox, both work and it just comes down to personal preference on the application and what you're use to.

Obviously your setup may differ depending on your system specs. I typically go with 4GB(4096 MB) of RAM per VM, 2 processors and 2 cores per processor but I am running with 32GB of RAM and an Intel i7-10750H.

If you need to, you can start with 4 or 8GB of RAM and 2 processors and 2 core per processor, for the install so it goes faster then drop it down to 2 or 4GB of RAM and 2 processors and 1 core per processor for the victim machines.

## Windows Server 2022

Starting with typical setup

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
