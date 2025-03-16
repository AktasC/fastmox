---
icon: box
---

# 20 - Container Setup

### Create your LXC

I won't go too much into detail here.\
Simply grab the latest Debian ISO and create an LXC that corresponds to your needs.\
I'll use Plex as an example of use case here so I'll setup my container accordingly.

* [x] Unprivileged container
* [x] Nesting

- Template: **Debian 12**
- Storage: **64Gb**
- Memory: **2048MB**

Don't forget to set both the IPv4/CIDR and Gateway addresses.

Don't run it immediately.

### LXC Configuration File

SSH into your node one last time.

Edit `/etc/pve/lxc/{yourContainersID}.conf` Add these lines:

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

Push the installer so you don't have to download it again.

```bash
pct push {yourContainerId} NVIDIA-Linux-x86_64-570.124.04.run /root/NVIDIA-Linux-x86_64-570.124.04.run
```

### LXC Setup

SSH into your freshly created LXC.

Install the <mark style="color:green;">Nvidiot</mark> drivers without kernel modules.

```bash
./NVIDIA-Linux-x86_64-570.124.04.run --no-kernel-module
```

* REFUSE when it asks for 32bit compability drivers
* REFUSE when asked if you want to update Xserver config.

### Reboot and enjoy hardware transcoding
