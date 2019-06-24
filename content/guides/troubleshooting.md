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

- Troubleshooting circuits: A common mistake is to have loose connection acros jumper wires or pins. A systematic way to identify and fix them is to check for continuity using a multimeter. Another common mistake is to have shorted or mismatched wiring (such as transistor based circuits), which can be identified by checking expected voltage at every connection.

- reef-pi uses the time settings from raspberry pi/raspbian. If timer are not acting as expected check if system time is configured correctly. Make sure timezone is configured correctly using **raspi-config**. 

- reef-pi API can be used for a variety of troubleshooting purpose, specifically when the UI is problematic. To use the API, use curl. reef-pi uses cookie based authentication, users have to create a auth cookie first and then use it for all further API based operations. API covers all aspects of reef-pi and powers the UI. Here is an example of listing number of equipments
```sh
curl -X POST -c cookie.txt -d '{"user":"reef-pi", "password":"reef-pi"}' http://reef-pi.local/auth/signin
curl -b cookie.txt http://reef-pi.local/api/equipment
```
API can be used to create backup, check a specific equipment, ato, ph probe etc, or to automate more complex workflows using ancillary scripts. 


- What information to share when asking for help? If you are still stuck, feel free to reach out to reef2reef thread on reef-pi. Please note down reef-pi version, Pi version, circuit details (an image will be very helpful) and shared those details while asking question. They help deducing the issues faster.


