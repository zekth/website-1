---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: Power controller build
title: How to build a power controller
highlight: true
weight: 1
---

Automated power strips allow on-demand and timer based control of AC outlets (110v or 220v). They are one of the easiest to build yet most useful controllers using reef-pi. Timers can be used to turn on/off light or skimmer daily. On-demand controls allow turning off equipments like ATO and return pump during water changes. It also involve minimal electronics and configuration among all other controller based on reef-pi. This build guide will go through step by step process of building a four outlet power strip controller based on reef-pi.

### Things to consider

- Relay types: Controlling high AC voltahes via Raspbwrry Pi involves relays. Relays can be opto-couplers, mechanical or solid state. Mechanical relays are cheapest, optocouplers are safest and expensive. Solid state relays are somewhere in the middle, safer and last longer than mechanical relays and cheaper, readily available that opto coupler.
- Number of channels: The number of channels in a relay board determines how many AC connections can be controller. Since we are building a 4 outlet powerstrip, we'll go with a 4 channel ssd relay. We'll need one GPIO pin of Raspberry Pi for each channel on the relay. It is possible to control around 18 channel relays using raspberry pi alone (it can be extend to thousands using an IO expander).


### Bill of Materials

- [Pi zero](https://www.adafruit.com/product/3400)
- [micro sd card](https://www.adafruit.com/product/2693)
- 4 Channel SSD relay. [example](https://www.amazon.com/gp/product/B00ZZVQR5Q/)
- 5v 2.4 amp [adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- AC Power adapter with fuse. [example](https://www.amazon.com/gp/product/B00ME5YAPK)
- AC Power cord. [example](https://www.amazon.com/gp/product/B00005113L/)
- AC receptacles [example](https://www.amazon.com/gp/product/B002DQT5UK/)
- Female female jumper wires. [example](https://www.amazon.com/gp/product/B00DJY4RS0)

### Wiring

![breadboard](/img/power_strip/breadboard.png)


### Install & Configure reef-pi

Follow reef-pi installation [guide](http://reef-pi.com/general-guides/07_install) to setup reef-pi on Raspberry Pi zero.

- Declare outlets and equipments

```yaml
outlets:
	AC1:
		pin: 4
  AC2:
    pin: 18
  AC3:
    pin: 14
  AC4:
    pin:
equipments:
   Heater: AC0
   Return: AC1
   Light: 
  
```
Note: the pin number represent the GPIO Pin number, not their position on the Raspberry Pi.


- Restart reef-pi

```
sudo systemctl restart reef-pi.service
```


### Usage

#### Controlling equipments on-demand

#### Controlling equipments using timers

