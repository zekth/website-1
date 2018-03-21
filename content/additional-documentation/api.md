---
author: "Ranjib Dey"
date: 2017-08-24
linktitle: api
title: API
highlight: true
weight: 4
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

reef-pi porvides a simple HTTP JSON based **A**pplication **P**rogramming **I**nterface. reef-pi web user interface itself is built using this API. API can be used to control reef-pi from an external system as well. Following is the reef-pi 1.0 API which will not have any breaking changes till the next major release (2.0). reef-pi 1.x series release may receive new features and corresponding API endpoints but all of the 1.0 API endpoints will be intact and not have any breaking changes. Breaking changes will require next major release.


### 1.0 API

reef-pi API uses basic authentication. HTTP requests must have associated headers to make successful API calls. Examples in this document assumes reef-pi is running on the same computer (127.0.0.1) with username and passowrd both set to 'reef-pi'.


API is categorized under a main controller specific group and several sub-system specific groups, where each sub-system represents a key responsibility such as lighting control or auto top off or temeperature control using sensors and equipents. reef-pi is modular and can be run with only a single or any combination of these modules enabled. Hence, module specific APIs are only available when these sub system is enabled. reef-pi UI reflects the same and shows only the module specific UI components.


#### Controller specific endpoints


##### GET /api/capabilities

Returns the currently enabled capabilities
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/capabilities
```
Response:
```json
{
  "dev_mode": true,
  "dashboard": true,
  "health_check": true,
  "equipments": true,
  "timers": true,
  "lighting": true,
  "temperature": true,
  "ato": true,
  "camera": true,
  "doser": true,
  "configuration": true
}
```

##### GET /api/settings

Returns current settings for the controller
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/settings
```
Response:
```json
{
  "name": "reef-pi",
  "interface": "wlan0",
  "address": "127.0.0.1:8080",
  "display": false,
  "notification": false,
  "capabilities": {
    "dev_mode": true,
    "dashboard": true,
    "health_check": true,
    "equipments": true,
    "timers": true,
    "lighting": true,
    "temperature": true,
    "ato": true,
    "camera": true,
    "doser": true,
    "configuration": true
  },
  "health_check": {
    "enable": false,
    "max_memory": 500,
    "max_cpu": 2
  }
}
```

##### POST /api/settings

Updates controller settings
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/settings
```
Payload:
```json
{
  "name": "reef-pi",
  "interface": "eth0",
  "address": "0.0.0.0:8080",
  "display": false,
  "notification": false,
  "capabilities": {
    "dev_mode": true,
    "dashboard": true,
    "health_check": true,
    "equipments": true,
    "timers": true,
    "lighting": true,
    "temperature": true,
    "ato": true,
    "camera": true,
    "doser": true,
    "configuration": true
  },
  "health_check": {
    "enable": false,
    "max_memory": 500,
    "max_cpu": 2
  }
}
```

##### POST /api/credentials

Updates username and password used to authenticate reef-pi API
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/credentials
```
Payload:
```json
{
  "user": "foo",
  "password": "bar"
}
```

##### GET /api/telemetry

Returns telemetry configuration, which includes adafruit.io and email account details. Passwords are always set to empty string.
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/telemetry
```
Response:
```json
{
  "adafruitio": {
    "enable": false,
    "token": "",
    "user": "",
    "prefix": ""
  },
  "mailer": {
    "server": "",
    "port": 0,
    "from": "",
    "password": "",
    "to": ""
  },
  "notify": false,
  "throttle": 0
}
```

##### POST /api/telemetry

Update telemetry configuration
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/telemetry
```
Payload:
```json
{
  "adafruitio": {
    "enable": false,
    "token": "",
    "user": "",
    "prefix": ""
  },
  "mailer": {
    "server": "",
    "port": 0,
    "from": "",
    "password": "",
    "to": ""
  },
  "notify": false,
  "throttle": 0
}
```

##### GET /api/health_stats/hour

Returns controller health stats (cpu and memory) every minute, for past three hours
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/health_stats/hour
```
Response:
```json
[
  {
    "cpu": 1.89,
    "memory": 51.37,
    "time": "Nov-22-09:31"
  },
  {
    "cpu": 1.94,
    "memory": 51.2,
    "time": "Nov-22-09:32"
  },
  {
    "cpu": 1.97,
    "memory": 51.53,
    "time": "Nov-22-09:33"
  },
  {
    "cpu": 1.96,
    "memory": 51.7,
    "time": "Nov-22-09:34"
  },
  {
    "cpu": 2.1,
    "memory": 52.03,
    "time": "Nov-22-09:35"
  }
]
```

##### POST /api/display/on

Turns on touchscreen display
```
curl -X POST -u reef-pi:reef-pi http://127.0.0.1:8080/api/display/on
```

##### POST /api/display/off

Turns off display.
```
curl -x POST -u reef-pi:reef-pi http://127.0.0.1:8080/api/display/off
```

##### GET /api/display

Returns the current bringness value of display
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/display
```
Response:
```json
{
 "on" : true,
 "brightness": 39
}
```

##### POST /api/display

Set brightness of display
```
curl -X POST -d@payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/display
```
Payload:
```json
{
 "on" : true,
 "brightness": 80
}
```

##### POST /api/admin/poweroff

Turn off reef-pi controller and the raspberry pi running it.
```
curl -X POST -u reef-pi:reef-pi http://127.0.0.1:8080/api/admin/poweroff
```

##### POST /api/admin/reboot

Reboot raspberry pi running reef-pi controller 
```
curl -X POST -u reef-pi:reef-pi http://127.0.0.1:8080/api/admin/reboot
```

##### POST /api/admin/reload
Reload reef-pi controller, without rebooting the Raspberry Pi (recommended after settings is updated)
```
curl -X POST -u reef-pi:reef-pi http://127.0.0.1:8080/api/admin/reload
```

##### GET /api/admin/info

Returns summary information about the controller such as IP and reef-pi version.
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/info
```
Response:
```json
{
  "name": "reef-pi",
  "ip": "10.0.0.10",
  "current_time": "Wed Nov 22 09:34:04",
  "uptime": "3 minutes ago",
  "cpu_temperature": "36.9C",
  "version": "1.0"
}
```


#### Connectors

Connectors represet all AC and DC output present in reef-pi. reef-pi 1.0 has two types of connectors; outlets for
AC equipment like heater, chiller, return pump etc, and jacks for dimmable DC equipment like LED lights, dosing pumps etc.

##### GET /api/outlets

Returns the list of outlets (AC socket)
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/outlets
```
Response:
```json
[
  {
    "id": "1",
    "name": "O1",
    "pin": 6,
    "equipment": "1",
    "reverse": false
  },
  {
    "id": "2",
    "name": "O2",
    "pin": 12,
    "equipment": "2",
    "reverse": false
  },
  {
    "id": "3",
    "name": "O3",
    "pin": 13,
    "equipment": "3",
    "reverse": false
  }
]
```

##### GET /api/outlets/_ID_

Returns details about a specific outlet
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/outlets/1
```
Response:
```json
{
  "id": "1",
  "name": "O1",
  "pin": 6,
  "equipment": "1",
  "reverse": false
}
```

##### PUT /api/outlets

Create an outlet
```
curl -X PUT -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/outlets
```
Payload:
```json
{
  "name": "O9",
  "pin": 12,
  "reverse": false
}
```

##### POST /api/outlets/_ID_

Update an existing outlet
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/outlets/1
```
Payload:
```json
{
  "name": "O9",
  "pin": 12,
  "reverse": true
}
```

##### DELETE /api/outlets/_ID_

Delete an existing outlet
```
curl -X DELETE -u reef-pi:reef-pi http://127.0.0.1:8080/api/1
```

##### GET /api/jacks

Returns list of jacks (DC PWM socket)
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/jacks
```
Response:
```json
[
  {
    "id": "1",
    "name": "J0",
    "pins": [ 0 ]
  },
  {
    "id": "2",
    "name": "J1",
    "pins": [ 1, 2 ]
  }
]
```

##### GET /api/jacks/_ID_

Returns details of an individual jack
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/jacks/1
```
Response:
```json
{
  "id": "1",
  "name": "J0",
  "pins": [ 0 ]
}
```

##### PUT /api/jacks

Create a new jack

```
curl -X PUT -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/jacks
```
Payload:
```json
{
  "name": "J2",
  "pins": [ 1,2 ]
```

##### POST /api/jacks/_ID_

Update an existing jack
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/jacks
```
Payload:
```json
{
  "name": "J3",
  "pins": [ 1,2 ]
}
```

##### DELETE /api/jacks/_ID_

Deletes an existing jack
```
curl -X DELETE -u reef-pi:reef-pi http://127.0.0.1:8080/api/jacks/1
```

#### equipments

##### GET /api/equipments

Returns list of equipment
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/equipments
```
Response:
```json
[
  {
    "id": "1",
    "name": "Return",
    "outlet": "1",
    "on": false
  },
  {
    "id": "2",
    "name": "Light",
    "outlet": "2",
    "on": false
  },
]
```

##### GET /api/equipments/_ID_

Returns details of an individual equipment
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/equipments/1
```
Response:
```json
{
  "id": "2",
  "name": "Light",
  "outlet": "2",
  "on": false
}
```

##### PUT /api/equipments

Create a new equipment
```
curl -X PUT -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/equipments
```
Payload:
```json
{
  "name": "TestEquipment",
  "outlet": "2",
  "on": false
}
```

##### POST /api/equipments/_ID_

Update an existing equipment
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/equipments/1
```
Payload:
```json
{
  "name": "TestEquipment",
  "outlet": "2",
  "on": true
}
```

##### DELEE /api/equipments/_ID_

Delete an existing equipment
```
curl -X DELETE -u reef-pi:reef-pi http://127.0.0.1:8080/api/equipments/1
```

#### timers

##### GET /api/timers

Returns list of all timers
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/timers
```
Response:
```json
[
  {
    "id": "1",
    "minute": "0",
    "day": "*",
    "hour": "20",
    "second": "0",
    "equipment": "3",
    "on": true,
    "name": "HeaterOn"
  }
]
```

##### GET /api/timers/_ID_

Returns details of an existing timer
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/timers/1
```
Response:
```json
{
  "id": "1",
  "minute": "0",
  "day": "*",
  "hour": "20",
  "second": "0",
  "equipment": "3",
  "on": true,
  "name": "HeaterOn"
}
```

##### PUT /api/timers

Create a new timer
```
curl -X PUT -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/timers
```
Payload:
```json
{
  "name": "HeaterOn",
  "day": "*",
  "hour": "20",
  "minute": "0",
  "second": "0",
  "on": true,
  "equipment": "3"
}
```

##### POST /api/timers/_ID_

Update an existing timer
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/timers/1
```
Payload:
```json
{
  "name": "HeaterOn",
  "day": "*",
  "hour": "20",
  "minute": "0",
  "second": "0",
  "on": true,
  "equipment": "4"
}
```

##### DELEE /api/timers/_ID_

Deletes an existing timer
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/
```


### ato

**A**uto **T**op **O**ff specific API, only available when ato capability is enabled

##### GET /api/ato

Returns ato configuration
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/ato
```
Response:
```json
{
  "sensor": 12,
  "pump": "6",
  "check_interval": 60,
  "control": true,
  "enable": true,
  "notify": {
    "enable": false,
    "max": 0
  }
}
```

##### POST /api/ato

Updates ato configuration
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/
```
Payload:
```json
{
  "sensor": 12,
  "pump": "6",
  "check_interval": 15,
  "control": true,
  "enable": true,
  "notify": {
    "enable": true,
    "max": 90
  }
}
```

##### GET /api/ato/usage

Returns hourly ato pump usage for last seven days. Pump value denotes number of seconds ATO pump was on during that hour
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/ato/usage
```
Response:
```json
[
  {
    "pump": 360,
    "time": "Nov-22-09:31"
  },
  {
    "pump": 240,
    "time": "Nov-22-10:13"
  }
]
```


#### lights

Light related API allows controlling dimmable LED lights using variable DC output(PWM). This API endpoints are only available if
lighting capability is enabled

##### GET /api/lights

Returns the list of lights
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/lights
```
Response:
```json
[
  {
    "id": "1",
    "name": "A360",
    "channels": {
      "1": {
        "name": "channel-1",
        "min": 0,
        "max": 100,
        "ticks": 12,
        "values": [ 0, 0, 0, 0, 29, 61, 38, 32, 20, 0, 0, 0 ],
        "fixed": 0,
        "auto": true,
        "reverse": false,
        "pin": 1
      },
    "jack": "1"
  }
]

```

##### GET /api/lights/_ID_

Returns details of an individual light.
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/lights/1
```
Response:
```json
{
  "id": "1",
  "name": "A360",
  "channels": {
    "1": {
      "name": "channel-1",
      "min": 0,
      "max": 100,
      "ticks": 12,
      "values": [ 0, 0, 0, 0, 29, 61, 38, 32, 20, 0, 0, 0 ],
      "fixed": 0,
      "auto": true,
      "reverse": false,
      "pin": 1
    },
  "jack": "1"
}
```

##### PUT /api/lights

Creates a new light
```
curl -X PUT -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/lights
```
Payload:
```json
{
  "name": "Kesiil-A80",
  "channels": {
    "1": {
      "name": "channel-1",
      "min": 0,
      "max": 100,
      "ticks": 12,
      "values": [ 0, 0, 0, 0, 29, 61, 38, 32, 20, 0, 0, 0 ],
      "fixed": 0,
      "auto": true,
      "reverse": false,
      "pin": 1
    },
  "jack": "1"
}
```

##### POST /api/lights/_ID_

Updates an existing light
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/lights/1
```
Payload:
```json
{
  "name": "A360",
  "channels": {
    "1": {
      "name": "channel-1",
      "min": 0,
      "max": 100,
      "ticks": 12,
      "values": [ 0, 0, 0, 0, 29, 61, 38, 32, 20, 0, 0, 0 ],
      "fixed": 20,
      "auto": false,
      "reverse": false,
      "pin": 1
    },
  "jack": "1"
}
```

##### DELETE /api/lights/_ID_

Deletes an existing light
```
curl -X DELETE -u reef-pi:reef-pi http://127.0.0.1:8080/api/lights/1
```

### Temperature controller

Temperature conroller API allows updating temperature controller configuration as well
as reading latest temperature and trends etc. These endpoints are only available when temeperature sub system is enabled.


##### GET /api/tc/config

Returns current temperature controller configuration
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/tc/config
```
Response:
```json
{
  "min": 78,
  "max": 80,
  "check_interval": 1,
  "heater": "3",
  "cooler": "5",
  "control": true,
  "enable": true,
  "dev_mode": false,
  "notify": {
    "enable": false,
    "min": 76,
    "max": 82
  }
}
```

##### POST /api/tc/config

Updates current temperature controller configuration
```
curl -X POST -d @payload -u reef-pi:reef-pi http://127.0.0.1:8080/api/tc/config
```
Payload:
```json
{
  "min": 78,
  "max": 80,
  "check_interval": 1,
  "heater": "3",
  "cooler": "5",
  "control": true,
  "enable": false,
  "dev_mode": false,
  "notify": {
    "enable": false,
    "min": 76,
    "max": 82
  }
}
```

##### GET /api/tc/readings

Returns the last 168 measurements from temperature sensor
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/tc/readings
```
Response:
```json
[
  {
    "time": "Nov-22-09:31",
    "temperature": 79.81
  },
  {
    "time": "Nov-22-09:32",
    "temperature": 79.31
  },
  {
    "time": "Nov-22-09:33",
    "temperature": 80.06
  }
]
```

##### GET /api/tc/usage

Returns hourly usage of heater, cooler and average of temperature readings for last 7 days
```
curl -u reef-pi:reef-pi http://127.0.0.1:8080/api/tc/usage
```
Response:
```json
[
  {
    "heater": 0,
    "cooler": 1,
    "time": "Nov-22-09:31",
    "temperature": 79.72
  }
]
```
