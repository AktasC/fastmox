---
description: I love my 2600X but there's a 1070 sitting at idle there ...
---

# 👾 GPU Passthrough

To use hardware encoding and decoding, and thus leave the CPU alone, we have multiple pre-requisites.

### BIOS

Ensure these features are enabled:

* AMD-VI
* Above 4G Decoding

### Host Setup

SSH into the **node** / baseInstall where Proxmox sits.

#### Preparation

Upgrade the system packages and install essential new ones.

```bash
apt update
apt upgrade -y
apt install pve-headers-$(uname -r) build-essential software-properties-common make nvtop htop -y
```

Now update grub & initramfs

```bash
update-grub
update-initramfs -u -k all
```

Download the latest Nvidiot x64 drivers, blacklist `nouveau` & reboot

```bash
wget "https://us.download.nvidia.com/XFree86/Linux-x86_64/570.124.04/NVIDIA-Linux-x86_64-570.124.04.run"
chmod +x ./NVIDIA-Linux-x86_64-570.124.04.run
```

```bash
systemctl reboot
```

#### Installation

Run the installer

```bash
./NVIDIA-Linux-x86_64-570.124.04.run --dkms
```

* ACCEPT when it offers to handle existing `nouveau`driver
* ACCEPT when it offers to `rebuild initrafms`
* REFUSE when it asks for 32bit compability drivers
* REFUSE when asked if you want to update Xserver config.

```bash
systemctl reboot
```

***

#### Optional - Blacklisting generic drivers

If for some reason the installation fails instead of gracefully handling existing drivers

```bash
echo -e "blacklist nouveau\nblacklist nvidia*\noptions nouveau modeset=0" > /etc/modprobe.d/blacklist-nouveau.conf
update-grub
update-initramfs -u -k all
systemctl reboot
```

Run the installation again

***

#### Verify the installation

```
ls -al /dev/nvidia*
```

If everything went well, you should see `/dev/nvidia0`and `/dev/nvidiactl`

Check if IOMMU is enabled:

```sh
dmesg | grep -e DMAR -e IOMMU -e AMD-Vi
```

Verify IOMMU interrupt remapping is enabled:

```sh
dmesg | grep 'remapping'
```

Check if VFIO is already enabled for some random reason:

```sh
lsmod | grep vfio
```

If not, we'll need to add three lines in `/etc/modules`

```bash
echo "vfio" >> /etc/modules
echo "vfio_iommu_type1" >> /etc/modules
echo "vfio_pci" >> /etc/modules
```

Once you're done, apply the changes:

```bash
update-initramfs -u -k all
systemctl reboot
```

Add these lines in `/etc/udev/rules.d/100-nvidia.rules`

```bash
KERNEL=="nvidia", RUN+="/bin/bash -c '/usr/bin/nvidia-smi -L && /bin/chmod 666 /dev/nvidia*'"
KERNEL=="nvidia_uvm", RUN+="/bin/bash -c '/usr/bin/nvidia-modprobe -c0 -u && /bin/chmod 0666 /dev/nvidia-uvm*'"
SUBSYSTEM=="module", ACTION=="add", DEVPATH=="/module/nvidia", RUN+="/usr/bin/nvidia-modprobe -m"
```

***

#### Optional - Persistence Services

To avoid the driver/kernel module getting unloaded whenever the GPU is unused.

```bash
cp /usr/share/doc/NVIDIA_GLX-1.0/samples/nvidia-persistenced-init.tar.bz2 .
```

```bash
bunzip2 nvidia-persistenced-init.tar.bz2
```

```bash
tar -xf nvidia-persistenced-init.tar
```

```bash
chmod +x nvidia-persistenced-init/install.sh;
./nvidia-persistenced-init/install.sh
```

```bash
rm -rf nvidia-persistenced-init*
```

***

#### LXC Configuration File

Edit `/etc/pve/lxc/101.conf` Add these lines:

```c
lxc.cgroup2.devices.allow: c 195:* rwm
lxc.cgroup2.devices.allow: c 234:* rwm
lxc.cgroup2.devices.allow: c 237:* rwm
lxc.mount.entry: /dev/nvidia0 dev/nvidia0 none bind,optional,create=file
lxc.mount.entry: /dev/nvidiactl dev/nvidiactl none bind,optional,create=file
lxc.mount.entry: /dev/nvidia-modeset dev/nvidia-modeset none bind,optional,create=file
lxc.mount.entry: /dev/nvidia-uvm dev/nvidia-uvm none bind,optional,create=file
lxc.mount.entry: /dev/nvidia-uvm-tools dev/nvidia-uvm-tools none bind,optional,create=file
lxc.mount.entry: /dev/nvidia-caps/nvidia-cap1 dev/nvidia-caps/nvidia-cap1 none bind,optional,create=file
lxc.mount.entry: /dev/nvidia-caps/nvidia-cap2 dev/nvidia-caps/nvidia-cap2 none bind,optional,create=file
```

### LXC Setup

```bash
wget "https://us.download.nvidia.com/XFree86/Linux-x86_64/570.124.04/NVIDIA-Linux-x86_64-570.124.04.run"
chmod +x ./NVIDIA-Linux-x86_64-570.124.04.run
```

```bash
sh ./NVIDIA-Linux-x86_64-570.124.04.run --no-kernel-module
```

* REFUSE when it asks for 32bit compability drivers
* REFUSE when asked if you want to update Xserver config.

### Reboot and enjoy hardware transcoding

***

### References

* [PCI Passthrough](https://pve.proxmox.com/wiki/PCI_Passthrough) - Proxmox Wiki&#x20;
* [PCI Passthrough via OVMF](https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF) - Arch Wiki&#x20;
* [Plex GPU transcoding in Docker on LXC on Proxmox](https://jocke.no/2022/02/23/plex-gpu-transcoding-in-docker-on-lxc-on-proxmox/) - Jocke.no&#x20;
* [The Ultimate Beginner's Guide to GPU Passthrough](https://www.reddit.com/r/homelab/comments/b5xpua/the_ultimate_beginners_guide_to_gpu_passthrough/) - Reddit&#x20;
* [Proxmox LXC GPU Passthru Setup Guide](https://digitalspaceport.com/proxmox-lxc-gpu-passthru-setup-guide/) - Digital Spaceport&#x20;
