---
icon: book
---

# 00 - Preparation

SSH into the **node** / baseInstall where Proxmox sits.

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

Download the latest <mark style="color:green;">Nvidiot</mark> drivers & reboot

```bash
wget "https://us.download.nvidia.com/XFree86/Linux-x86_64/570.124.04/NVIDIA-Linux-x86_64-570.124.04.run"
chmod +x ./NVIDIA-Linux-x86_64-570.124.04.run
```

```bash
systemctl reboot
```
