---
author: "Ranjib Dey"
date: 2019-07-03
linktitle: API
title: API
highlight: true
weight: 20
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
- api
---

## API V3

### Authentication

  POST	/auth/signin
   GET	/auth/signout
  POST	/api/credentials
   GET	/api/me

### Core configuration

   GET	/api/info
   GET	/api/capabilities
   GET	/api/settings
  POST	/api/settings
   GET	/api/telemetry
  POST	/api/telemetry
  POST	/api/telemetry/test_message
   GET	/api/dashboard
  POST	/api/dashboard
DELETE	/api/errors/clear
DELETE	/api/errors/ID
   GET	/api/errors/ID
   GET	/api/errors
   GET	/api/health_stats
   GET	/api/pwm_profiles/ID
   GET	/api/pwm_profiles
   PUT	/api/pwm_profiles
DELETE	/api/pwm_profiles/ID
  POST	/api/pwm_profiles/ID

### Rasoverry Pi

#### Power cycle

  POST	/api/admin/poweroff
  POST	/api/admin/reboot
  POST	/api/admin/reload
   
#### Display control

  POST	/api/display/on
  POST	/api/display/off
  POST	/api/display
   GET	/api/display

### Electronics

#### Drivers

   GET	/api/drivers
   GET	/api/drivers/ID
   PUT	/api/drivers
DELETE	/api/drivers/ID
  POST	/api/drivers/ID

#### Connectors

   GET	/api/outlets/ID
   GET	/api/outlets
   PUT	/api/outlets
DELETE	/api/outlets/ID
  POST	/api/outlets/ID
   GET	/api/inlets/ID
   GET	/api/inlets
   PUT	/api/inlets
DELETE	/api/inlets/ID
  POST	/api/inlets/ID
  POST	/api/inlets/ID/read
   GET	/api/jacks
   GET	/api/jacks/ID
   PUT	/api/jacks
  POST	/api/jacks/ID
DELETE	/api/jacks/ID
  POST	/api/jacks/ID/control
   GET	/api/analog_inputs
   GET	/api/analog_inputs/ID
   PUT	/api/analog_inputs
  POST	/api/analog_inputs/ID
DELETE	/api/analog_inputs/ID
  POST	/api/analog_inputs/ID/read

### Equipment 

   GET	/api/equipment/ID
   GET	/api/equipment
   PUT	/api/equipment
  POST	/api/equipment/ID
DELETE	/api/equipment/ID
  POST	/api/equipment/ID/control

### ATO

   GET	/api/atos/ID
   GET	/api/atos
   PUT	/api/atos
  POST	/api/atos/ID
DELETE	/api/atos/ID
   GET	/api/atos/ID/usage

#### Lights

   GET	/api/lights
   PUT	/api/lights
   GET	/api/lights/ID
  POST	/api/lights/ID
DELETE	/api/lights/ID

#### Temperature controllers

   GET	/api/tcs
   GET	/api/tcs/sensors
   PUT	/api/tcs
   GET	/api/tcs/ID
  POST	/api/tcs/ID
DELETE	/api/tcs/ID
   GET	/api/tcs/ID/usage

#### pH Probes

   GET	/api/phprobes/ID
   GET	/api/phprobes
   PUT	/api/phprobes
  POST	/api/phprobes/ID
DELETE	/api/phprobes/ID
   GET	/api/phprobes/ID/readings
  POST	/api/phprobes/ID/calibrate
   GET	/api/phprobes/ID/read
  POST	/api/phprobes/ID/calibratepoint

#### Dosing pumps`

   GET	/api/doser/pumps
   GET	/api/doser/pumps/ID
   PUT	/api/doser/pumps
  POST	/api/doser/pumps/ID
DELETE	/api/doser/pumps/ID
   GET	/api/doser/pumps/ID/usage
  POST	/api/doser/pumps/ID/calibrate
  POST	/api/doser/pumps/ID/schedule

#### Timers

   GET	/api/timers/ID
   GET	/api/timers
   PUT	/api/timers
  POST	/api/timers/ID
DELETE	/api/timers/ID

##### Macros

   GET	/api/macros
   PUT	/api/macros
   GET	/api/macros/ID
  POST	/api/macros/ID
DELETE	/api/macros/ID
  POST	/api/macros/ID/run

#### Camera

   GET	/api/camera/config
  POST	/api/camera/config
  POST	/api/camera/shoot
   GET	/api/camera/latest
   GET	/api/camera/list
