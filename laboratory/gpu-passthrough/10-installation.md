---
icon: terminal
---

# 10 - Installation

### Run the installer

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

### Verify the installation

```
ls -al /dev/nvidia*
```

If everything went well, you should see `/dev/nvidia0`and `/dev/nvidiactl`&#x20;

Run `nvtop` to double-check.

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

Add these lines in `/etc/udev/rules.d/100-nvidia.rules`

```bash
KERNEL=="nvidia", RUN+="/bin/bash -c '/usr/bin/nvidia-smi -L && /bin/chmod 666 /dev/nvidia*'"
KERNEL=="nvidia_uvm", RUN+="/bin/bash -c '/usr/bin/nvidia-modprobe -c0 -u && /bin/chmod 0666 /dev/nvidia-uvm*'"
SUBSYSTEM=="module", ACTION=="add", DEVPATH=="/module/nvidia", RUN+="/usr/bin/nvidia-modprobe -m"
```

Once you're done, apply the changes:

```bash
update-initramfs -u -k all
systemctl reboot
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
