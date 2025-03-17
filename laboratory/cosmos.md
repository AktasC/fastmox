# 🌌 Cosmos

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
