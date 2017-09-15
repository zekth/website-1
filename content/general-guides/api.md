---
author: "Ranjib Dey"
date: 2017-08-24
linktitle: api
title: Application Programmers Interface
highlight: true
weight: 5
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

### Operating system

reef-pi can be developed on linux, OS X and windows. The physical control part can only be run on linux. reef-pi in particular been tested and developed on raspbian running on Raspberry Pi.

reef-pi software architecture composed of three main components
- A physical backend: Part that controls physical devices (pwm, relay, sensor)
- A HTTP server: Part that converts the physical control part to reef hobby specific terms.
- UI: JavaScript specific user interface, or the code that is executed in browers, depending upon where the reef-pi user is this code is run on that computer (or mobile devices)

### Database

reef-pi uses [boltdb], a [go] based key,value database. All configuration data (lights, equipments, atos etc) is stored in a single bolt database file. Telemetry data (historical values of sensors, lighting) that is used for charting/graphing is sent to adafruit.io and not stored on the bolt database. reef-pi users can backup the boltdb file present on the microSD card, for redundancy.

### Configuration files

reef-pi uses a configuration file to boot and control a handful of critical settings about reef-pi. Configuration file is specified in [YAML]() specification. Configuration file is located at /etc/reef-pi/config.yaml. Since reef-pi is under heavy development the configration file format is changing frequently, this will be stabilied as part of 1.0 release. Specific configuration file for any version can be found at build/reef-pi.yaml location of the repository.


### Protocols

reef-pi porvides a simple HTTP JSON based interface. Following is a list of currently available endpoints. A note of caution, till reef-pi hits 1.0 release the API is likely to undergo a lot of changes. 1.0 will mark the first major release, which signifies 1.0 API will not have any breaking change (that is consumers will always work on 1.0 based releases, it can have new improvements, but it cant remove anything existing, or change it in a way that impacts users directly) for 1 year.


#### API Endpoints

##### GET /api/capabilities
##### GET /api/settings
##### POST /api/settings

##### GET /api/equipments/{id}
##### GET /api/equipments
##### GET /api/equipments
##### GET /api/equipments
##### GET /api/equipments

##### GET /api/outlets

##### GET /api/lights

##### GET /api/jacks

