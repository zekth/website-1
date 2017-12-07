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

Water level sensors such as photoelectric sensor or float switches acts as electrical switches, they are turned off normally and when turn on when submerged in water. One of the Raspberry Pi's GPIO is wired to a water level sensor and reef-pi is configured to check this GPIO state periodically. When reef-pi detects the GPIO pn is in **off** state it turns on the specified equipment (ATO pump) which pours fresh RO/DI water into the tank. When water level reach, the GPIO returns **on** state again, and reef-pi turns off the ATO pump. reef-pi check frequency (normally set to 1 minute) determines the minimum amount of time the ATO pump will be run.


### Things to consider

- Photoelectric sensor or float switch: Both of these sensors acts as switch and returns **off** when in air  and **on** when submerged in water. Hence reef-pi does not need any special configuration for them and they can be used in place of the other. But they work very differently. Photoelectric sensors are costler than floatswitches, require additional elctronics to work, and are not prone to salt creep. While, flotswitches are inexpensive, requires no additional circuit, can be easily sourced, but prone to salt creep. We recommend using photoelectric sensor. The recommended [Bill of Materials](/general-guides/bom) contains a sample photoelectric sensor.

- ATO pump: These are used to pour fresh RO/DI water (without salt) in the tank to bring up the water level. Consider how you want to position the water resorvoir, ATO pump have to lift water to the required height. It is also important to consider the volume of water the ATO pump will pour per check interval (set to 1 minute by default), it should not be too much compared to the volume of the tank, else salinity will fall.


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

- Follow reef-pi installation [guide](/general-guides/install) to setup reef-pi on Raspberry Pi zero.
- Enable ATO capability from **Configuration** tab, reload reef-pi.
- Refresh your browser after reload. This will bring up the ATO tab. At this point ATO feature is enabled, but ATO sensor are not polled periodically.
- Click on the **Enable** checkbox under ATO tab. This will instruct reef-pi to start monitoring ATO sensor via GPIO pin number 12. If you have wired ATO sensor (or correspoinding connector) to a different GPIO pin, then update the **Sensor Pin** pin to reflect correct value.
- Click on the **control** checkbox to instruct reef-pi switch on ATO pump when Select the ATO pump from the equipment drop down. Without this, the ATO sub system will only monitor the sensor, but will turn on/off the pump.
- You can also turn on notification on pump usage. Pump usage is a numeric value that represent number of seconds pump was on every hour. For, example, if ATO is configure with a check interval of 2 minutes, ATO pump usage will be in multiple of 120 (2 * 60 seconds)


### Resources

[dfrobot's wiki](https://www.dfrobot.com/wiki/index.php/Liquid_Level_Sensor-FS-IR02_SKU:_SEN0205)
