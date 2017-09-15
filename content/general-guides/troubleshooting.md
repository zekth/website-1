---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: Troubleshooting
title: How to troubleshoot and ask for help
highlight: true
weight: 4
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

- Check if reef-pi is running

```
sudo ystemctl status reef-pi.service
```

- Check for errors in log

```
sudo journalctl -fu reef-pi.service
```

- Connecting reef-pi using a TTL cable. Adafruit has an excellent [tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all) on how to use USB TTL cable to configure raspberry pi, in cases where display and keyboard is not available.


- Check reef-pi version (helps in bug reports)

```
reef-pi -version
```

- Resetting reef-pi 's data base

```
sudo systemctl stop reef-pi.service
sudo rm -rf /var/lib/reef-pi/reef-pi.db
sudo ststemctl start reef-pi.service
```


