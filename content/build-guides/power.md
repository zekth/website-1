---
linktitle: power
title: How to build a power controller
highlight: true
weight: 1
---

Automated power strips allow on-demand and timer based control of AC outlets (110v or 220v). They are one of the easiest to build yet most useful controllers using reef-pi. For example: a power controller can turn on/off light or skimmer daily as well as allow on-deman controls like switching off ATO and return pump during water changes. This guide will go through step by step process of building a four outlet power controller.

### Things to consider

- Which relay to use? Controlling high AC voltages via Raspbwrry Pi involves relays. Relays can be opto-couplers, mechanical or solid state. Mechanical relays are cheapest, optocouplers are safest and expensive. Solid state relays are somewhere in the middle, safer and last longer than mechanical relays and cheaper, readily available that opto coupler.

- Relay capacity: Almost all relays are rated to work with a voltage and current range. Most mechanical relays are raterd for 10 amp, 240volt ac, while solid state relays are generally rater for 240volt ac, 2 amp. Depending upon what type of equipment you will be powering, choose appropriate relays. Equipments are generally rated with watts, and watt = volt x ampere. i.e. a 100 watt heater will rquire at least 1 amp relay to be powered safely by 110volt ac.

- Number of relay channels: The number of channels in a relay board determines how many AC connections can be controller. Since we are building a 4 outlet powerstrip, we'll go with a 4 channel ssd relay. We'll need one GPIO pin of Raspberry Pi for each channel on the relay. It is possible to control around 18 channel relays using raspberry pi alone (it can be extend to thousands using an IO expander).


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

Follow reef-pi installation [guide](http://reef-pi.com/general-guides/install) to setup reef-pi on Raspberry Pi zero.

- Declare outlets and equipments

```yaml
outlets:
  AC1:
    pin: 17
  AC2:
    pin: 27
  AC3:
    pin: 22
  AC4:
    pin: 24
equipments:
   Heater: AC1
   Return: AC2
   Light:  AC3
   Filter: AC4
```

Note: the pin number represent the GPIO Pin number, not their position on the Raspberry Pi. Refer Raspberry Pi pinout [diagram](http://www.jameco.com/Jameco/workshop/circuitnotes/raspberry_pi_circuit_note_fig2.jpg) for GPIO numbers.


- Restart reef-pi

```
sudo systemctl restart reef-pi.service
```
Thats it, you should be able to access reef-pi user interface from the browser and control all four equipments.

### Usage

#### Controlling equipments on-demand

Any equipment specified in the configurartion file can be switched on or off any time using reef-pi web interface. Use the equipment tab to navigate to the list of equipments and click on the on/off button to switch the equipment on/off. Every equipment should have a dedicated button indicating the equipment's real time state.

![on-demand ui](/img/power_strip/on-demand.png)

#### Controlling equipments using timers

In the following example we are setting up heater to start at night 10:00 PM and stop at morning 6:00 AM. Use the "Jobs" tab to define two jobs. Each job represent a period action reef-pi takes. 

The first job starts the heater at night. reef-pi allowes us to specify which equipment to take action against, time details (day of the month, hour, minute, second etc) and the action (on or off). Notice "\*" is used to denote every day of the month.

![timer start](/img/power_strip/timer_start.png)

And another job to stop the heater every morning 6 AM.

![timer start](/img/power_strip/timer_stop.png)

reef-pi uses cron style specification for denoting time schedule, this allows much more elaborate way of specifying schedules, check the [timer](http://reef-pi.com/build-guides/timer) guide for details.
