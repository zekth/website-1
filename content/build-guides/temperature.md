---
author: "Ranjib Dey"
date: 2017-09-27
linktitle: temperature
title: Temperature controller
highlight: true
weight: 4
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
- temperature controller
- iot
---

Maintaining a stable temperature is a key requirement for a thriving reef tank. Most reef tanks maintain a stable temperature within 77 to 80 degree fahrenheit for optimal coral growth. Depending upon the environment where reef tank is located this might require cooling down the tank using a chiller or heating it up with a heater. Because environmental temperature varies during day and night at most places, reef tank temperature is often monitored and controlled automatically using a controller. Heaters are also most frequently failed equipments in reef tank, leading to tank crash. Temperature controllers are helps in avoiding such catastrophic situation as well.

In this guide we'll be using reef-pi to build a temperature controller that will monitor the temperature of reef tank and turn on heater or cooler when the temperature goes above or below a specified range.

### How it works

reef-pi can monitor reef tank temperature using a DS18B20 temperature probe. The temperature controller inside reef-pi can be configured to check this sensor value periodically and if its goes above or below a certain range, reef-pi can switch on or off a specified heating or cooling equipment. Generally a heater is used as a heating equipment and fan or chiller is used as a cooling equipment.

### Things to consider

- Temperature probe: There are many types of DS18B20 probes available. Go for the ones that are made for sub-merged usage. Also pay attention to the outer coating material. Most submercible ds18b20 probes are made of steel but often time they show rust within first couple of months of usage. There are way to rust proof them without significantly altering the probing capability, like using a [heat shrink tube](https://www.adafruit.com/product/1020) or [plasti dip](https://www.amazon.com/dp/B00I9SK8XY/) or silicone dip. But there are also other submercible probes (like the ones from canakit and sparkfun) which had black coating around them, they last longer but costlier compared to the bare steel probes.

- Heater and cooler choice: reef-pi internally only control relays which in turn control the cooling or heating equipment. In most cases heaters are used as heating equipment. Generally, it is recommendedto have two to five watts per gallon worth heating capacity, i.e. a 30 gallong tank should use at least an 100 watt heater. Multiple heaters can be used to for a single tank. For cooling, if the ambient temperature is not more than 3 to four degrees higher, fans work. Otherwise, a chiller is a best option.


### Bill of materials

- [Pi zero](https://www.adafruit.com/product/3400) or [Pi 3](https://www.adafruit.com/product/3055)
- [micro sd card](https://www.adafruit.com/product/2693)
- 5v 2.4 amp [power adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- [DS18B20 temperature probe](https://www.amazon.com/dp/B01B27R21Y/)
- Relay, with at least 2 channels [example](https://www.amazon.com/dp/B00E0NTPP4)
- AC receptacles [example](https://www.amazon.com/gp/product/B002DQT5UK/)
- [3.5mm female, panel mount audio jack](https://www.amazon.com/dp/B013AP77T8)
- [3.5mm male audio jack](https://www.amazon.com/dp/B00MFRZ2SG/)
- [Jumper wires](https://www.amazon.com/dp/B00DJY4RS0)

### Wiring

![breadboard](/img/temperature/breadboard.png)


### Installation & Configuration

- Follow reef-pi installation [guide](../../general-guides/install) to setup reef-pi on Raspberry Pi zero.

- Connect DS18B20

- Enable temperature capability under system tab

- Enabling temperature monitoring 

- Enabling temperature control

### Resources

- Adafruit [tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-11-ds18b20-temperature-sensing?view=all) on ds18b20 probe and Raspberry pi
- [Fritzing project file](https://github.com/reef-pi/DesignFiles/raw/master/temperature.fzz)
