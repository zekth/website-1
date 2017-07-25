---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: Troubleshooting
title: How to troubleshoot and ask for help
highlight: true
weight: 4
---

Check if reef-pi is running

```
sudo ystemctl status reef-pi.service
```

Check for errors in logA

```
sudo journalctl -fu reef-pi.service
```

Connecting reef-pi using a TTL cable
