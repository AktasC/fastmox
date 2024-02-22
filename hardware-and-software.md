---
description: >-
  Description of the hardware in my home server and the software I'm planning to
  use.
---

# Hardware & Software

## Hardware

For a long time, I've used my main rig as a home server&#x20;

After upgrading my main rig with a 5800X3D (I'm really milking the AM4 platform as much as I can), I upgraded my brother's rig with my old 3700X, which in turn left me alone with a 2600X.

This made me check for spare parts I had laying around and, lo and behold, I had pretty much everything I needed except for the case and RAM.\
(I didn't want to reuse the wraith coolers, not even the Max, so I also got the TR Peerless Assassin)

All of the hardware listed below sits in a cute little Jonsbo D41 Mesh :heart:

<table data-header-hidden><thead><tr><th width="158"></th><th></th></tr></thead><tbody><tr><td>CPU</td><td>AMD Ryzen 5 2600X</td></tr><tr><td>Cooler</td><td>ThermalRight Peerless Assassin 120</td></tr><tr><td>Motherboard</td><td>Asus TUF Gaming B450M-Plus II</td></tr><tr><td>RAM</td><td>2 x G.Skill Trident Z Neo 16G @3600MHz CL16</td></tr><tr><td>GPU</td><td>Asus GTX 1070 Dual</td></tr><tr><td>Fast Storage</td><td>Crucial P3 Plus 1To M.2 NVMe </td></tr><tr><td>Bulk Storage</td><td>2 x Western Digital Blue 4T HDD @7200RPM </td></tr></tbody></table>

## Software Stack

My home server has two purposes:

* Running a 24/7 Plex server for my family, with remote access and HW acceleration.
* Experimenting as a software engineer.

### Plex

For the Plex part of this equation, I will keep things simple:

The base system will be an Ubuntu LXC provided by @tteck which will have GPU passthrough for those sweet concurrent 4K streams.

The content media will be cloned from "RD" using `rclone` with `zurg` .\
This way, I only have symlinks to the RD webdav and don't need to store everything locally.

### Cosmos-Cloud

Alright, so this might be the most controversial part but hear me out:

**Portainer is great** and offers a whole set of tools when it comes to container management, I've used it for many months on my main rig with an `*arr` cluster and several other services.\
The reason why I didn't want to go the Portainer route this time is simple: I'm getting old and lazy.\
I don't need all of the tools Portainer is providing, and I'll already have enough to do with the experiments I want to conduct anyways, so why add weight to an otherwise pretty slim setup ?

A lot of people talk about [CasaOS](https://casaos.io/), which is a distribution developed by [Zima Board](https://www.zimaboard.com/).\
I've used it for two weeks, in a privileged LXC, with Plex and other services running on it and, honestly, it was a pretty good experience.\
But, this time, the problem is that I can't help but feel like it's not secure enough and not hackable / customisable enough.\
I'm aware that [ZimaOS](https://github.com/IceWhaleTech/zimaos-rauc) is currently under development and will address the remote access & authentication weaknesses of CasaOs, but it's nowhere near a public release.\
I will keep an eye on it, but for now I need something a bit more mature.

Without further ado, enter [Cosmos-Cloud](https://cosmos-cloud.io/).\
In a few words, Cosmos comes with an integrated VPN and reverse proxy, 2FA and SSO authentication solutions, a more granular container management system and a bigger "marketplace".\
Suffice to say it looks and feels a bit more serious than CasaOS.

