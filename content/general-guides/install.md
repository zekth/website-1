---
author: "Ranjib Dey"
date: 2017-07-25
linktitle: Installation
title: Install & configuration
highlight: true
description: Installation and configuration of reef-pi controller
weight: 1
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

This guide will walk you through the process of installing and configuring reef-pi on a Raspberry Pi. The entire installation process involves three main stages.

- Creating a MicroSD card for Raspberry Pi
- Starting Raspberry Pi and configuring it to be used with  reef-pi
- Install and configuration of reef-pi on the Raspberry Pi

This guide assume some prior familiarity with computers, but no programming knowledge is required.

### Prepare Raspberry Pi image

We recommend a microSD card of Class10 and at least 8Gb capacity for reef-pi. reef-pi is tested on raspbian, but it should work on most other linux OS, on Raspberry Pi. Follow the official raspberry pi guide for details instructions:
- [Download and write raspbian image to micro SD card](https://www.raspberrypi.org/documentation/installation/installing-images/)

### Connecting to Raspberry Pi

You can either use console cable or an HDMI based display (monitor or TV) to access raspberry pi.

For console access setup follow [this adafruit tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all). HDMI based access is fairly easy, just hook up any HDMI enabled display (monitor or TV) to raspberry pi using an HDMI cable.


### Configure raspberry pi

Once raspbian image is written on microSD card, plug it in Raspberry Pi and power it. Once Raspbian OS is started, configure following things internet, date and ssh access.

- Configure wifi: Enabling wifi or ethernet based internet connection allows reef-pi to be accessible from any web browser (mobile, tablet or computers). Note, this is not a mandatory requirement, reef-pi can run without any internet connectivity. This is for convenience, to allow accessing reef-pi web interface from any other devices, such as laptop, tablets or mobile phones. Detailed steps for wifi configuration is available [here](https://www.raspberrypi.org/documentation/configuration/wireless/)


- Use the terminal window to perform a system update with the following command. Note: Skip this step if internet is not enabled.

```
sudo apt-get update -y
sudo apt-get upgrade -y
```

- Change password: Raspbian images comes with a stock password for the "pi" user. Reset it to something unique and stronger

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

- Configure ssh: ssh is used to remotely control and troubleshoot the Raspberry Pi.

```
sudo systemctl start ssh.service
sudo systemctl enable ssh.service
```
- Set time and date: Configure raspbian to use network time to synchronize its date & time information. Also set specific locale, to reflect the local time instead of UTC

```
sudo systemctl start systemd-timesyncd.service
sudo systemctl enable systemd-timesyncd.service
sudo dpkg-reconfigure tzdata
```

Finally, reboot Raspberry Pi to apply all the kernel configuration changes

```
sudo reboot
```

Most of these steps can  be done using graphical interface as well,

  - Click the Raspberry Pi icon in the upper left.
  - Go to Preferences -> Raspberry Pi Configuration
  - On the Interfaces tab enable the necessary items (time, localization etc)


### Install reef-pi

- Once  Raspberry Pi is up and running,  navigate to the reef-pi release page and copy link for the latest [release](https://github.com/reef-pi/reef-pi/releases)
- Make sure you choose the right release package for Raspberry Pi 3 or pi zero.
- Open Terminal and type following commands to download and  install reef-pi, assuming you are installing 1.0 release

```
wget -c https://github.com/reef-pi/reef-pi/releases/download/1.0/reef-pi-1.0-pi3.deb
sudo dpkg -i reef-pi-1.0-pi3.deb
```

- Check reef-pi is running

```
sudo systemctl status reef-pi.service
```


Thats it, after this, you should be able to access reef-pi from the browser

Default reef-pi login username and password both is set as **reef-pi**. Update these from the settings section under conifiguration tab. You can play areound with the UI to get familiar with it. Next, use the [electronics & wiring guide](/general-guides/electronics) to setup all the electronics components.

