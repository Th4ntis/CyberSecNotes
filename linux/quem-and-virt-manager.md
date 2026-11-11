# QUEM and Virt-Manager

## QEMU & Virt-Manager

Notes on virtualization with QEMU/KVM and the Virt-Manager GUI, plus a ready-to-go Kali VM setup. **Virtualization** lets you run a complete guest operating system in a window on your host - ideal for testing distros, running a throwaway lab machine, or keeping risky work (like security tooling) isolated from your main system.

The typical stack has three layers that are easy to confuse:

* **KVM** - the Linux kernel's built-in hardware virtualization. It's what makes\
  guests run at near-native speed, and it's a kernel feature, not a program you\
  launch.
* **QEMU** - the emulator/virtualizer that actually runs the guest. On matching\
  hardware it hands the heavy lifting to KVM.
* **libvirt** - a management layer with a consistent API and tools, which\
  Virt-Manager (and `virsh` on the command line) drive on your behalf.

In short: Virt-Manager talks to libvirt, which drives QEMU, which uses KVM.

### QEMU

#### About

QEMU is a generic and open-source machine emulator and virtualizer. Used as a **machine emulator**, QEMU can run OSes and programs built for one architecture (e.g. an ARM board) on a different one (e.g. your x86 PC) through dynamic translation. Used as a **virtualizer** - paired with KVM on matching hardware - it runs guests of the _same_ architecture at near-native speed. That\
second mode is what you'll use most on a normal PC.

#### Links

* [Homepage](https://www.qemu.org/download/#linux)
* [Docs](https://www.qemu.org/documentation/)
* [Wiki](https://wiki.qemu.org/Main_Page)

#### Install (Debian/Ubuntu)

```bash
sudo apt install -y qemu-system qemu-user-static
```

#### Verify your system supports virtualization

Check that the CPU exposes virtualization extensions - you should see `Virtualization: VT-x` (Intel) or `Virtualization: AMD-V` (AMD):

```bash
lscpu | grep Virtualization
```

> If nothing shows up, hardware virtualization may be disabled in your BIOS/UEFI\
> (often labeled **VT-x**, **AMD-V**, or **SVM**) - enable it there first. Without\
> it, QEMU still runs but falls back to slow software emulation.

Verify KVM is available (`kvm-ok` comes from the `cpu-checker` package on Debian/Ubuntu: `sudo apt install cpu-checker`):

```bash
sudo kvm-ok
```

### Virt-Manager

#### About

Virt-Manager (the "Virtual Machine Manager") is a desktop UI for managing virtual machines through libvirt. It primarily targets KVM VMs but can also manage Xen and LXC (Linux containers). It shows a summary of running domains with live performance and resource stats, provides wizards to create new VMs and adjust their virtual hardware, and includes an embedded VNC/SPICE viewer for a full graphical console to the guest. It's the easiest way to get going before dropping down to raw `qemu-system-…` commands like the Kali example below.

#### Links

* [Virt-Manager Homepage](https://virt-manager.org/)

#### Install (Debian/Ubuntu)

```bash
sudo apt install -y virt-manager
```

Add your user to the `libvirt` group so you can manage VMs without `sudo`\
(log out and back in afterward for it to take effect - this is the same\
group-membership mechanic described in Permissions and sudo > Part 2 - sudo):

```bash
sudo usermod -aG libvirt $USER
```

Then open the application to view and create VMs:

Pasted image 20260705215426.png

### Vagrant and Ansible

[Vagrant](https://www.vagrantup.com/) automates building and provisioning VMs from a `Vagrantfile` - so a whole machine (OS, packages, config) can be defined in code and spun up with one command. It can use libvirt/QEMU as its backend.

Install prerequisites:

```bash
sudo apt install -y vagrant libvirt-dev qemu-kvm libvirt-daemon-system
```

Install the libvirt provider plugin for Vagrant:

```bash
vagrant plugin install vagrant-libvirt
```

([Ansible](https://www.ansible.com/) is the natural companion for provisioning - describing, in YAML, what should be installed and configured once the VM is up.)

### Kali VM (QEMU directly)

An example of creating and running a Kali Linux VM with QEMU on the command line, with a shared folder between host and guest. This is the "no GUI" path - useful when you want a scripted, repeatable VM.&#x20;

Create the virtual disk (60 GB; `qcow2` grows on demand rather than\
pre-allocating the full size):

```bash
qemu-img create -f qcow2 kali.qcow2 60G
```

Launch the VM with a shared folder (`virtfs`/9p). On first boot, boot from the installer ISO (`-boot d`):

```bash
qemu-system-x86_64 \
  -enable-kvm -cpu host -smp 4 -m 4G \
  -drive file=kali.qcow2,if=virtio \
  -nic user,model=virtio-net-pci \
  -device virtio-vga -display gtk \
  -virtfs local,path=/home/you/shared,mount_tag=hostshare,security_model=mapped-xattr,id=hostshare \
  -cdrom /home/th4ntis/SynologyDrive/Damian/Software-ISO/kali-linux-2026.2-installer-amd64.iso -boot d
```

> Flags in brief: `-enable-kvm` uses hardware acceleration, `-cpu host` exposes your real CPU features to the guest, `-smp 4` gives 4 vCPUs, `-m 4G` gives 4 GB RAM, and the `virtio` devices are the fast paravirtualized disk/network/video. After installation, drop the `-cdrom`/`-boot d` line so it boots from the installed disk instead of the ISO.

Mount the shared folder inside Kali:

```bash
sudo mkdir -p /mnt/shared
sudo mount -t 9p -o trans=virtio,version=9p2000.L,msize=104857600 hostshare /mnt/shared
```

To mount it automatically on boot, add an entry to `/etc/fstab` inside the guest (editing system files like this needs root - see Permissions and sudo):

```
hostshare  /mnt/shared  9p  trans=virtio,version=9p2000.L,msize=104857600  0  0
```
