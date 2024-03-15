---
description: I love my 2600X but there's a 1070 sitting at idle there ...
---

# PCI Passthrough

To use hardware encoding and decoding, and thus leave the CPU alone, we have multiple pre-requisites.

### BIOS

Ensure AMD-Vi is enabled

### OS

SSH into the node / baseInstall where Proxmox sits.

#### Setup VFIO

Check if VFIO is already enabled for some random reason:

```sh
lsmod | grep vfio
```

If not, we'll need to add three lines in `/etc/modules`

```
vfio
vfio_iommu_type1
vfio_pci
```

Once you're done, apply the changes:

<pre class="language-sh"><code class="lang-sh"><strong> update-initramfs -u -k all
</strong></code></pre>

After that, reboot and ssh back into it.

#### IOMMU

Verify IOMMU is enabled:

```sh
dmesg | grep -e DMAR -e IOMMU -e AMD-Vi
```

Verify IOMMU interrupt remapping is enabled:

```sh
dmesg | grep 'remapping'
```

#### GPU Drivers

```sh
echo "blacklist nouveau" >> /etc/modprobe.d/blacklist.conf 
echo "blacklist nvidia*" >> /etc/modprobe.d/blacklist.conf 
```

```sh
apt update; apt dist-upgrade -y
```
