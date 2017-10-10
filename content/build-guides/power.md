---
linktitle: power
title: Power controller
highlight: true
weight: 1
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- iot
- relay
---

Automated power strips allow on-demand and timer based control of AC outlets (110v or 220v). They are one of the easiest to build yet most useful controllers using reef-pi. For example: a power controller can turn on/off light or skimmer daily as well as allow on-demand controls like switching off ATO and return pump during water changes. This guide will go through step by step process of building a four outlet power controller.

### How this work

reef-pi software uses Raspberry Pi's GPIO pins to control digital relays, which in turn controls  high voltage, high current AC or DC equipments. This mechanism is used across timer or sensor based (like temperature or ato controllers) equipment controls. 

### Things to consider

- Choice of relay: Controlling high AC voltages via Raspberry Pi involves relays. Relays can be optocouplers, mechanical or solid state. Mechanical relays are cheapest, optocouplers are safest and expensive. Solid state relays are somewhere in the middle, safer, more expensive and last longer than mechanical relays but cheaper more readily available that optocoupler. We recommend optocoupler based relays where price is not a factor, solid state relays where current requirements are low (less than 2 amp) and mechanical relays for beginners or anything else. 

- Relay capacity: Almost all relays are rated to work with a voltage and current range. Most mechanical relays are rated for 10 amp, 240volt ac, while solid state relays are generally rated for 240volt ac, 2 amp. Depending upon what type of equipment you will be powering, choose appropriate relays. Equipments are generally rated with watts, and watt = volt x ampere. i.e. a 100 watt heater will require at least 1 amp relay to be powered safely by 110volt ac.

- Number of relay channels: The number of channels in a relay board determines how many AC connections can be controller. Since we are building a 4 outlet powerstrip, we'll go with a 4 channel ssd relay. We'll need one GPIO pin of Raspberry Pi for each channel on the relay. It is possible to control around 18 channel relays using raspberry pi alone (it can be extend to thousands using an IO expander).


### Bill of Materials

- [Pi zero](https://www.adafruit.com/product/3400)
- [micro sd card](https://www.adafruit.com/product/2693)
- 5v 2.4 amp [adapter](https://www.adafruit.com/product/1995) for Raspberry Pi
- 4 Channel SSD relay. [example](https://www.amazon.com/gp/product/B00ZZVQR5Q/)
- AC Power adapter with fuse. [example](https://www.amazon.com/gp/product/B00ME5YAPK)
- AC Power cord. [example](https://www.amazon.com/gp/product/B00005113L/)
- AC receptacles [example](https://www.amazon.com/gp/product/B002DQT5UK/)
- Female-female jumper wires. [example](https://www.amazon.com/gp/product/B00DJY4RS0)

### Wiring

![breadboard](/img/power/breadboard.png)


### Install & Configure reef-pi

- Follow reef-pi installation [guide](/general-guides/install) to setup reef-pi on Raspberry Pi zero.

- Enable equipment capability and turn off dev mode under setting section on system tab


![capability](/img/power/capability.png)

- Click on the *update* button to save settings followed by *reload* button to ensure the changes are loaded immediately. Refresh your browser (since reef-pi is reloading, it may take few seconds). You should see equipments tab now.

- Navigate to system tab again and declare outlets. Use the GPIO pin numbers (*not serial number*) to define one outlet per relay channels. You can use the recommend pinout scheme to decide which GPIOs to use. They should mimic the exact wiring.


![add outlet](/img/power/outlet_add.png)

- Since this guide follows a four channel relay, we are declaring 4 outlets.

![add outlets](/img/power/outlet_all.png)


Note: the pin number represents the GPIO Pin number, not their position on the Raspberry Pi. Refer Raspberry Pi pinout [diagram](http://www.jameco.com/Jameco/workshop/circuitnotes/raspberry_pi_circuit_note_fig2.jpg) for GPIO numbers.

- The outlet declaration is one-time work; it will not change unless electronics are updated.

- Next declare equipments under the equipment tab. Each equipment should have an assigned outlet. 

![add equipment](/img/power/add_equipment.png)

- Since we have four outlets in this build, we are declaring four essential equipments for a pico reef tank.
![all equipment](/img/power/all_equipment.png)

That's it, you should be able to use reef-pi to control all four equipments.

### Usage

#### Controlling equipments on-demand

Any equipment specified in the configuration file can be switched on or off any time using reef-pi web interface. Use the equipment tab to navigate to the list of equipments and click on the on/off button to switch the equipment on/off. Every equipment should have a dedicated button indicating the equipment's real-time state.

![on-demand ui](/img/power/on-demand.png)

#### Controlling equipments using timers

Timers in reef-pi allows automation of an action on a equipemnt at a given schedule.

In the following example we are setting up heater to start at night 10:00 PM and stop at morning 6:00 AM. Use the "timers" tab to define two timers. Each timer represents a period action reef-pi takes. 

The first job starts the heater at night. reef-pi allows us to specify which equipment to take action against, time details (day of the month, hour, minute, second etc) and the action (on or off). Notice "\*" is used to denote every day of the month.

![timer start](/img/power/timer_start.png)

And another job to stop the heater every morning 6 AM.

![timer start](/img/power/timer_stop.png)

reef-pi uses cron style specification for denoting time schedule, this allows much more elaborate way of specifying schedules. 

A typical schedule specifies day and time related details for the timer.

reef-pi uses [cron](https://en.wikipedia.org/wiki/Cron) like specification to define timer schedules.

Following is a summary of the specification

- "day of month" represent which day of every month the job will be triggered. Values can range from 1 to 31
- "hour" represent which hour of the day job will be triggered. Values can range from 0 to 23
- "minute" represent which minute of the hour job will be triggered. Value can range from 0 to 59
- "second" represent which second of the minute job will be triggered. Values can range from 0 to 59


Other than their mentioned ranges, each of this field can also take few special entries.

They are:

- "\*" represents **every** . Like every hour, every day etc
- "-" to represent **ranges**. Example: hour can be "2-6" to trigger a job every hour from 2 to 6
- "/" to represent **after every**. Example: Hour value "\*/3" represents after every 3 hours

More details can be found in  the underlying library's [documentation](https://godoc.org/github.com/robfig/cron#hdr-CRON_Expression_Format)

Timers can be used to automate use cass like two part dosing, refugium light etc.

### Resources

- [Fritzing project file](https://github.com/reef-pi/DesignFiles/raw/master/PowerStrip.fzz)

