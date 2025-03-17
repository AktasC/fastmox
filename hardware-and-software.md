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

Also, I've never used Proxmox prior to February 2024.\
Deciding between PVE, UnRaid and TrueNAS wasn't an easy decision to make.

* Why not UnRaid ?\
  I have a shiny NVMe SSD I want to boot from.\
  Who's the genius behind the "your boot drive needs to be a USB flash drive" idea ?
* Why not TrueNAS then ?\
  Honestly, it looked like a really nice option but I'm not going to use this server as a NAS, and the storage I have on hand is pretty limited for today's standards anyways.

### Plex

For the Plex part of this equation, I will keep things simple:

The base system will be an Ubuntu LXC, generated using the script provided by @tteck (R.I.P), with GPU passthrough for those sweet and smooth concurrent 4K streams.

#### Why not Jellyfin ? It's way better in every way !

Because I have a lifetime Plex pass and everyone's devices at home are already setup.\
In short, don't fix what's not broken lmao.

### Zurg & RClone

The content media will be cloned from Real-Debrid using rclone with zurg.\
[Zurg ](https://github.com/debridmediamanager/zurg-testing)uses your RD apiToken and regexes to make your movies & shows available through a webDav server.\
[RClone ](https://rclone.org/)is used to mount this webDav server as storage into your file system.\
This way, I only have symlinks to my Real-Debrid cache and don't need to store anything locally.

### AMP

This one is pretty simple to explain: I've got a bunch of friends with whom I enjoy CS (been playing CS since 1.6), Astroneer, Satisfactory and Palworld among other games, for which I would like to have dedicated servers I can manage and mod at will.

I've tried setting up Pterodactyl and it worked well for some games but ended up causing me more trouble than I was willing to solve so I switched to [AMP](https://cubecoders.com/AMP).

### AdGuard Home

Since I didn't have any prior experience in this field, I had a wide variety of choice when it comes to ad blocking.\
You could use Pi-Hole or any other solution but I chose AdGuard for how performant yet easy to deploy, customize and maintain it is.

### Bitwarden

I know a lot of you probably expect to hear that I'm going to use [Vaultwarden ](https://github.com/dani-garcia/vaultwarden)but that's not the case.\
At least not in this point in time.

I have nothing but :heart: for Rust, the language not the org, as [@ThePrimeagen](https://www.twitch.tv/ThePrimeagen) and other influencial devs showed its qualities many times.

I just don't want to go into community-made alternatives or rather I'd like to have the most vanilla / simple experience possible.\
Especially when the product I'm trying to self-host has documentation on how to do just that, stable and updated docker images and provably good developers working on it.

