---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: Troubleshooting
title: Troubleshooting
highlight: true
weight: 12
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

- Check if reef-pi is running

```
sudo systemctl status reef-pi.service
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

- Resetting reef-pi's database

```
sudo systemctl stop reef-pi.service
sudo rm -rf /var/lib/reef-pi/reef-pi.db
sudo systemctl start reef-pi.service
```

- One of the common reason gotcha is dev_mode being enabled. Dev mode allows reef-pi development in non-raspberry pi system and it mask all physical control (they are faked out). Make sure dev_mode is disabled or unchecked, under **Configuration -> Settings -> Capabilities**. Note: changing any of the capabilities will require a reload to take effect.

- Check if time is configured correctly: All of reef-pi timers and almost all periodic tasks rely on system time. Make sure timezone is configured correctly using **raspi-config**.


- What information to share when asking for help? If you are still stuck, feel free to reach out to reef2reef thread on reef-pi. Please note down reef-pi version, Pi version, circuit details (an image will be very helpful) and shared those details while asking question. They help deducing the issues faster.


- Troubleshooting circuits: Check voltage at every connection. Ends of jumper pins. Check for continuity before wiring.
