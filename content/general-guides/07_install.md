---
author: "Ranjib Dey"
date: 2017-07-25
linktitle: Installation
title: How to install reef-pi on Raspberry Pi
highlight: true
weight: 7
---

### Prepare Raspberry Pi image

- Download raspbian image
- Write raspbian image to micro SD card

### Configure raspberry pi

- Configure wifi
- Update system
- Change password
- Enable i2c,onewire,spi,uart
- Configure and enable ssh

### Install reef-pi

- Download latest reef-pi release
- Install reef-pi

```
dpkg -i reef-pi-<version>.deb
```
- Check reef-pi is running

```
systemctl status reef-pi.service
```

### Configure reef-pi

- Enable accessing UI from other devices

```yaml
address: 0.0.0.0:8080
```
- Define outlets

