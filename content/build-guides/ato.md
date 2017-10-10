---
linktitle: ato
title: Auto Top Off
highlight: true
weight: 3
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- iot
- ato
- auto top off
- auto top up
- coral
---

Automatic top off units are systems that maintain a constant water volume inside a reef tank. Reef tanks undergoe water evaporation which results in loss of water volume, which in turn increases the salinity of remaining water. Corals are highly sensitive to salinity thus unless the evaporated water is supplemented with fresh RO/DI water it will have a detrimental effect to corals. Auto top off units monitors water level periodically and when it falls below a certain level, they switch on an ATO pump to replenish the lost water volume with fresh RO/DI water, till it reaches the expected volume. The degree of water evaporation is dependent on several factors like ambient temperature,  whether the tank has open top or  closed lid, if a fan is used to cool down tanks etc. The effect of water loss due to evaporation is dependant on tank size. Our communal understanding is smaller tanks such as nano and pico reefs,  require ATO more than bigger tanks. A stable water height is also important for optimal skimmers performance.

This build guide will cover how to build an inexpensive yet effective auto top off unit using reef-pi.

### How this work

### Things to consider

- photo electric sensor or float switch

- ATO pump


### Bill of materials

- [Pi zero](https://www.adafruit.com/product/3400) or [Pi 3](https://www.adafruit.com/product/3055)
- [micro sd card](https://www.adafruit.com/product/2693)
- 5v 2.4 amp [power adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- Relay, with at least 1 channel [example](https://www.amazon.com/dp/B00E0NTPP4)
- [Photo electric liquid level sensor](https://www.amazon.com/dp/B074T9WHGF/)
- [Submersible water pump](https://www.amazon.com/dp/B073VSZH2P/)
- [12v DC power adapter](https://www.amazon.com/dp/B01ICSD93Q/) for ATO pump
- AC receptacles [example](https://www.amazon.com/gp/product/B002DQT5UK/)
- [3.5mm female, panel mount audio jack](https://www.amazon.com/dp/B013AP77T8)
- [3.5mm male audio jack](https://www.amazon.com/dp/B00MFRZ2SG/)
- [Jumper wires](https://www.amazon.com/dp/B00DJY4RS0)

### Wiring

![breadboard](/img/ato/breadboard.png)

### Installation & Configuration

- Follow reef-pi installation [guide](../../general-guides/install) to setup reef-pi on Raspberry Pi zero.


### Resources

[dfrobot's wiki](https://www.dfrobot.com/wiki/index.php/Liquid_Level_Sensor-FS-IR02_SKU:_SEN0205)
