---
description: I love my 2600X but there's a 1070 sitting at idle there ...
---

# 👾 GPU Passthrough

To use hardware encoding and decoding, and thus leave the CPU alone, we have multiple pre-requisites.

### BIOS

Before anything else, ensure these features are enabled in your BIOS:

* AMD-VI
* Above 4G Decoding

### Host Setup

#### Preparation

{% content-ref url="00-preparation.md" %}
[00-preparation.md](00-preparation.md)
{% endcontent-ref %}

#### Installation

{% content-ref url="10-installation.md" %}
[10-installation.md](10-installation.md)
{% endcontent-ref %}

***

### LXC Setup

{% content-ref url="20-container-setup.md" %}
[20-container-setup.md](20-container-setup.md)
{% endcontent-ref %}

### References

* [PCI Passthrough](https://pve.proxmox.com/wiki/PCI_Passthrough) - Proxmox Wiki&#x20;
* [PCI Passthrough via OVMF](https://wiki.archlinux.org/title/PCI_passthrough_via_OVMF) - Arch Wiki&#x20;
* [Plex GPU transcoding in Docker on LXC on Proxmox](https://jocke.no/2022/02/23/plex-gpu-transcoding-in-docker-on-lxc-on-proxmox/) - Jocke.no&#x20;
* [The Ultimate Beginner's Guide to GPU Passthrough](https://www.reddit.com/r/homelab/comments/b5xpua/the_ultimate_beginners_guide_to_gpu_passthrough/) - Reddit&#x20;
* [Proxmox LXC GPU Passthru Setup Guide](https://digitalspaceport.com/proxmox-lxc-gpu-passthru-setup-guide/) - Digital Spaceport&#x20;
