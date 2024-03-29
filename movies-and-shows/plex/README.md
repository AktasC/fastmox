# 🎥 Plex

For simplicity's sake I'll be using[ @tteck's scripts for Proxmox-VE](https://tteck.github.io/Proxmox/)

```bash
bash -c "$(wget -qLO - https://github.com/tteck/Proxmox/raw/main/ct/plex.sh)"
```

This will create an LXC dedicated to Plex Media Server and allocate it 2G of RAM, 8G of storage and 2 vCores by default.\
Personally, I'll adjust the allocated ressources such as:

* RAM: 4096 MB
* SWAP: 2048 MB
* Storage: 128 GB
* CPU: 6 vCores

While I'll locally store symlinks to the files on Real-Debrid, and thus shouldn't need that much storage, there might be times where Plex pulls the whole file for media analysis among other things.\
That, and the way RClone & Zurg work are the reason why I bumped up both the vCPU, RAM, Swap and storage allocations.\
For example, I've seen the LXC briefly spike up to 6.3GB of RAM usage by times, though the average usage for the past week's orbiting around 1GB.

***

Through the Proxmox GUI:

* `Options` section
* Click on `Features`
* Enable `FUSE`

Once you're done, head to the `console`

```bash
# Installing basic tools.
apt-get update; apt-get dist-upgrade -y; apt-get install curl git micro
```

```bash
micro /etc/ssh/sshd_config
```

Set `PermitRootLogin` to `yes`&#x20;
