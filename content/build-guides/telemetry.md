---
author: "Ranjib Dey"
date: 2017-07-21
linktitle: Telemetry
title: Telemetry
highlight: true
weight: 5
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

Telemetry module in reef-pi allow users to capture sensor and controller health data and alert based on it. Telemetry functionality helps us to avoid tank accidents due to equipment failure (such as a bad heature cooking up tank) or to understand long term trends in tank parameters. This guide will walk through the basic telemetry features and how to configure them. This guide assumes you have a running reef-pi controller already. Follow the [general guides](/general-guides/) first  if you do not have a working reef-pi installation.

### Sending telemetry data to adafruit.io

reef-pi allows emitting telemetry data to adafruit.io. The data can be used visulaize trends for longer periods (a month or two) over internet (i.e. even outside home wifi where reef-pi UI is not accessible). This data is persistent and unlike the built in dashboatd, it is avialble even when reef-pi controller is powered off. Following are the steps to setup Adafruit.io integration:

1. Signup for Adafruit.io account
2. Obtain Adafruit.io token
3. Configure reef-pi with adafruit.io and enable telemetry. Reload reef-pi
4. Build dashboards with your reef tank data from reef-pi at Adafruit.io

### Setting up email alerts

1. Enable notification under Configuration -> Telemtry.
2. Specify email settings.


### reef-pi dashboard

reef-pi controller comes with its own in-built dashboard that charts past seven days of telemetry data and few other relevant information. This data is transient and is lost everytime reef-pi controller is restarted. The dashboard reconfigures itself automatically based on the capabilities enabled (Configuration -> Settings -> Capabilities). Inside reef-pi dashboard feature itself modeled as an capability, and can be enabled or disabled from the configuration tab. Following is a brief overview of the charts provided in the dashboard and what they reflect:

1. Equipment: The equipment chart is a [bar chart](https://en.wikipedia.org/wiki/Bar_chart) where each vertical bar represent one equipment and the color of the bar indicates whether the equipment is on (green color) or off (gray).

2. Temperature: There are two temperature chart in the dashboard. First one shows past 180 readings and the second one shows hourly usage of temperature control device (heater and cooler) for past seven days along with average temperature. If temperature controller is configure to check sensor after every one minute, the first chart will show last three hours temperature. Temperature charts help us understand temperature fluctuation in the tank as well as how efficient heater cooler device to adjust tank temperature.

3. ATO: The ato chart shows hourly ato pump usage, where the usage metric stands for total number of seconds ato pump was turned on. ATO chart can be used to understand the evaporation rate and ATO pumps capability to how quickly it can adjust the water level.

4. Lighting: The lighting charts are made of one chart for each light. Each chart has one line per channel lighting values. For fixed value lightin (i.e. lights that are not under day light cycle or **auto** mode), these charts are not useful.

5. Controller health: This chart shows past seven days CPU and Memory usage of the controller. We recommend to run reef-pi under 1/3rd of the CPU/Memory usage. i.e. For Raspberry Pi 3 based controller normal CPU usage should not go above 0.3 and normal Memory usage should not go above 300 MB. This gives enough room for scenarios when the controller has to work harder, even with double amount of load, it will have 1/3rd of spare cpu/memory. Generally CPU and memory is usage increases with individual subsystem being enabled, higher number of equipment being controller or higher frequency of sensor checks.

