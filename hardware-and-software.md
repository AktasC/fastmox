---
description: >-
  Description of the hardware in my home server and the software I'm planning to
  use.
---

# 🛠️ Hardware & Software

## Hardware

For a long time, I've used my main rig as a home server&#x20;

After upgrading my main rig with a 5800X3D (I'm really milking the AM4 platform as much as I can), I upgraded my brother's rig with my old 3700X, which in turn left me alone with a 2600X.

This made me check for spare parts I had laying around and, lo and behold, I had pretty much everything I needed except for the case and RAM.\
(I didn't want to reuse the wraith coolers, not even the Max, so I also got the TR Peerless Assassin)

<table data-header-hidden><thead><tr><th width="158"></th><th></th></tr></thead><tbody><tr><td>Case</td><td>Jonsbo D41 Mesh <span data-gb-custom-inline data-tag="emoji" data-code="2764">❤️</span></td></tr><tr><td>CPU</td><td>AMD Ryzen 5 2600X</td></tr><tr><td>Cooler</td><td>ThermalRight Peerless Assassin 120 <span data-gb-custom-inline data-tag="emoji" data-code="2764">❤️</span></td></tr><tr><td>Motherboard</td><td>Asus TUF Gaming B450M-Plus II</td></tr><tr><td>RAM</td><td>2 x G.Skill Trident Z Neo 16GB @3600MHz CL16 </td></tr><tr><td>GPU</td><td>Asus GTX 1070 Dual 8GB</td></tr><tr><td>Fast Storage</td><td>Crucial P3 Plus 1To M.2 NVMe </td></tr><tr><td>Bulk Storage</td><td>2 x Western Digital Blue 4T HDD @7200RPM </td></tr></tbody></table>

## Software Stack

My home server has two purposes:

* Running a 24/7 Plex server for my family, with remote access and HW acceleration.
* Experimenting as a software engineer.

### Proxmox

There's a world where I would have setup everything on a barebone Debian netinstall.\
Another world in which I would have gone the TrueNAS ...

But. Remember. _C O N V E N I E N C E_&#x20;

* Built-in backups & snapshots
* Running multiple VMs and LXCs with a few clicks.
* Web-based GUI, which makes management a breeze.

Also, I never used Proxmox before February 2024.\
Deciding between it, UnRaid and TrueNAS wasn't an easy decision to take.

The reason I didn't go the UnRaid route is simple: I have a shiny NVMe SSD I want to boot from.\
Who's the genius behind the "your boot drive needs to be a USB flash drive" idea ?

TrueNAS on the other hand looked like a really nice option but I'm really not going to use this server as a NAS, and the storage I have on hand is pretty limited anyways.

### Plex

For the Plex part of this equation, I will keep things simple:

The base system will be an Ubuntu LXC provided by @tteck which will have GPU passthrough for those sweet sweet concurrent 4K streams.

#### Why not Jellyfin ? It's way better in every way !

Because I have a lifetime Plex pass and everyone's devices are already setup.\
In short, don't fix what's not broken lmao.

#### Zurg & RClone

The content media will be cloned from Real-Debrid using rclone with zurg.\
Zurg uses your RD apiToken and regexes to make your movies & shows available through a webDav server.\
RClone is used to mount this webDav server into your file system.\
This way, I only have symlinks to my Real-Debrid caches and don't need to store anything locally.

### Cosmos-Cloud

#### Why use Cosmos and not X ?

Oookay, soooo this might be the most controversial part, but hear me out.

**Portainer is great** and offers a comprehensive set of tools when it comes to container management, I've used it for many months on my main rig with an `*arr` stack and several other services.\
The reason why I didn't want to go the Portainer route this time is simple: I'm getting old and lazy.\
I don't require all of the tools Portainer is providing, and I'll already have enough to do with the experiments I want to conduct anyways, so why add weight to an otherwise pretty slim setup ?

A lot of people also talk about [CasaOS](https://casaos.io/), which is a distribution developed by [Zima Board](https://www.zimaboard.com/).\
I've used it for two weeks, in a privileged LXC container, with Plex and other services running on it and, honestly, it was an overall positive experience.\
But, this time, the problem is that I can't help but feel it lacked security and customisation options.\
&#x20;   I'm aware that [ZimaOS](https://github.com/IceWhaleTech/zimaos-rauc) is currently under development, and that it will address the remote access & authentication weaknesses of CasaOs, but it's nowhere near a public release state yet.\
I will keep an eye on it though, but for now I need a more mature solution.

Enter [Cosmos-Cloud](https://cosmos-cloud.io/).

Simply put, Cosmos includes an integrated VPN and reverse proxy, 2FA and SSO authentication solutions, a more granular container management system and a larger "marketplace."\
To me, it looks and feels a like a beefier CasaOS.

### Pterodactyl

This one is pretty simple to explain: I've got a bunch of friends with whom I enjoy CS and Palworld among other games, for which I would like to have dedicated servers. &#x20;

Pterodactyl works well with SteamCMD and doesn't seem to suffer the same issues as AMP when it comes to running in an LXC (VMs and barebone installs are the prefered way apparently).

That being said, Ptero really isn't the easiest to run and maintain from what I've read & heard, so this might change in the future.

### Bitwarden

I know a lot of you probably expect to hear that I'm going to use Vaultwarden but that's not the case.\
At least not in this point in time.

I have nothing but :heart: for Rust, as the GOAT [@ThePrimeagen](https://www.twitch.tv/ThePrimeagen) showed its qualities many times.

I just don't want to go into community-made alternatives or rather I'd like to have the most vanilla / simple experience possible.\
Especially when the product I'm trying to self-host has documentation on how to do just that, stable and updated docker images and provably good developers working on it.

