---
description: I love my 2600X but there's a 1070 sitting at idle there ...
---

# 👾 GPU Passthrough

To use hardware encoding and decoding, and thus leave the CPU alone, we have multiple pre-requisites.

### BIOS

Ensure AMD-Vi / Intel Vtd is enabled

### Host Setup

SSH into the node / baseInstall where Proxmox sits.

#### Preparation

```bash
echo -e "blacklist nouveau\noptions nouveau modeset=0" > /etc/modprobe.d/blacklist-nouveau.conf
```

Check if VFIO is already enabled for some random reason:

```sh
lsmod | grep vfio
```

If not, we'll need to add three lines in `/etc/modules`

```bash
vfio
vfio_iommu_type1
vfio_pci
```

Once you're done, apply the changes:

```bash
update-initramfs -u -k all
```

Check if IOMMU is enabled:

```sh
dmesg | grep -e DMAR -e IOMMU -e AMD-Vi
```

Verify IOMMU interrupt remapping is enabled:

```sh
dmesg | grep 'remapping'
```

```bash
apt purge nvidia-*
```

```bash
reboot
```

```bash
apt update; apt dist-upgrade;
apt install proxmox-headers-$(uname -r)
```

#### Installation

```bash
wget -O nvidia-550.67.run https://us.download.nvidia.com/XFree86/Linux-x86_64/550.67/NVIDIA-Linux-x86_64-550.67.run
```

```bash
chmod +x nvidia-550.67.run
# If you want to check the package before running it
# ./nvidia-550.67.run --check

./nvidia-550.67.run
# answer "NO" when it asks if you want to install 32bit compability drivers
# answer "NO" when it asks if it should update X config
```

```bash
echo -e '\n# load nvidia modules\nnvidia-drm\nnvidia-uvm' >> /etc/modules-load.d/modules.conf
```

Add these lines in `/etc/udev/rules.d/100-nvidia.rules`

```bash
KERNEL=="nvidia", RUN+="/bin/bash -c '/usr/bin/nvidia-smi -L && /bin/chmod 666 /dev/nvidia*'"
KERNEL=="nvidia_uvm", RUN+="/bin/bash -c '/usr/bin/nvidia-modprobe -c0 -u && /bin/chmod 0666 /dev/nvidia-uvm*'"
SUBSYSTEM=="module", ACTION=="add", DEVPATH=="/module/nvidia", RUN+="/usr/bin/nvidia-modprobe -m"
```

#### Persistence Service (Optional)

To avoid that the driver/kernel module is unloaded whenever the GPU is unused.

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
wget -O nvidia-550.67.run https://us.download.nvidia.com/XFree86/Linux-x86_64/550.67/NVIDIA-Linux-x86_64-550.67.run
```

```bash
chmod +x nvidia-550.67.run
# If you want to check the package before running it
# ./nvidia-550.67.run --check

./nvidia-550.67.run --no-kernel-module
# answer "NO" when it asks if you want to install 32bit compability drivers
# answer "NO" when it asks if it should update X config
```

### Reboot and enjoy hardware transcoding



### References

* [https://pve.proxmox.com/wiki/PCI\_Passthrough](https://pve.proxmox.com/wiki/PCI\_Passthrough)
* [https://wiki.archlinux.org/title/PCI\_passthrough\_via\_OVMF](https://wiki.archlinux.org/title/PCI\_passthrough\_via\_OVMF)
* [https://jocke.no/2022/02/23/plex-gpu-transcoding-in-docker-on-lxc-on-proxmox/](https://jocke.no/2022/02/23/plex-gpu-transcoding-in-docker-on-lxc-on-proxmox/)
* [The Ultimate Beginner's Guide to GPU Passthrough](https://www.reddit.com/r/homelab/comments/b5xpua/the\_ultimate\_beginners\_guide\_to\_gpu\_passthrough/)
