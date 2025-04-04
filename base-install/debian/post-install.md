---
description: >-
  Basic stuff that you shouldn't forget but let's put it there while we're at
  it.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: true
---

# Post Install

After installing Proxmox, you'll need to set it up a bit through the web UI.\
Once you're done, ssh into the proxmox install.

```shell
# Update sources, upgrade packages, install basic packages
$ apt update; apt dist-upgrade -y; apt install lm-sensors micro curl
```

_I'm not using nvim, wanna fight about it ?_

```bash
update-alternatives --set editor /usr/bin/micro
```

***

You could also use @tteck's Proxmox VE Post Install Script:&#x20;

```bash
bash -c "$(wget -qLO - https://github.com/tteck/Proxmox/raw/main/misc/post-pve-install.sh)"
```
