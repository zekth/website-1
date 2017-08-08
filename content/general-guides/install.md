---
author: "Ranjib Dey"
date: 2017-07-25
linktitle: Installation
title: How to install reef-pi on Raspberry Pi
highlight: true
weight: 1
---

This guide will walk you throug the process of installing and configuring reef-pi in a new Raspberry Pi with a new microSD card. The process involves three main part, first we have to prepare the micorsd card for Raspberry Pi, then start Raspberry Pi with the microSD card and configure it for reef-pi usage, and then finally install and configuration of reef-pi on the freshly prepared Raspberry Pi. This guide assume prior familiarity with computers, no programming knowledge is required.

### Prepare Raspberry Pi image

We recommend a microSD card of Class10 and atleast 8Gb capacity for reef-pi. reef-pi is tested on raspbian, but it should work on most other linux OS, on Raspberry Pi. Follow the official raspberry pi guide for details instructions:
- [Download and write raspbian image to micro SD card](https://www.raspberrypi.org/documentation/installation/installing-images/)

### Configure raspberry pi

Oncei raspbian image is written on microSD card, plug it in Raspberry Pi and power it. Once started configure following things at leat, for optimal performance of reef-pi.

- Configure wifi: Enabling wifi or ethernet based internet connection allows reef-pi to be accessible from any web browser (mobile, tablet or computers). Note, this is not a manadatory requirement for running wifi. It is just a convenience.

Next set of steps assume you are working on terminal:
- Update system: Perform a system update with following command. Note: if internet is not enabled, this will not work, and should be skipped.
```
sudo apt-get update -y
sudo apt-get upgrade -y
```

- Change password: Raspbian images comes with stock password for the "pi" user. Reset it to something unique and stronger

```
passwd
```
- Enable i2c,onewire,spi,uart: Different types of electronics in reef-pi requires a number of kernel modules and device drivers to be loaded in kernel. Edit `/boot/config.txt` to load these modules

```
dtparam=i2c_arm=on
dtparam=spi=on
dtparam=audio=on
enable_uart=1
dtoverlay=w1-gpio
```

- Configure and enable ssh: ssh is used to remotely control and troubleshoot the Raspberry Pi directly.

```
sudo systemctl start ssh.service
sudo systemctl enable ssh.service
```
- Set time and date: Configure raspbian to use network time to synchronize its date & time information. Also set specific locale, to reflect the local time instead of UTC

```
sudo systemctl start ntp.service
sudo systemctl enable ntp.service
sudo dpkg-reconfigure locales
```

Finally, reboot Raspberry Pi to apply all the kernel configuration changes

```
sudo reboot
```

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
