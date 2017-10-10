---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: upgrade
title: Upgrade
highlight: true
weight: 2
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

- Determine appropriate reef-pi version based on raspberry pi (3 or zero) from the [release](https://github.com/reef-pi/reef-pi/releases/) page. Choose latest relase if you are unsure. For this documentation we'll use 1.0 release version on pi zero.

- ssh into raspberry pi, running reef-pi and upgrade using following commands in a terminal

- Download the release package on reef-pi
```
wget -c https://github.com/reef-pi/reef-pi/releases/download/0.5/reef-pi-1.0-pi0.deb
```

- Remove the existing reef-pi
```
sudo apt-get remove reef-pi -y -f --purge
```

- Install the downloaded reef-pi version
```
sudo dpkg -i reef-pi-1.0-pi0.deb
```

- Check reef-pi is running suscessfully using
```
sudo systemctl status reef-pi.service
```

- reef-pi new version should be visible from the UI as well (under system tab)
