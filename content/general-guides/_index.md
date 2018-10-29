---
author: "Ranjib Dey"
date: 2017-07-21
---

This section provides a very high level overview of the build process and ongoing operation of a reef-pi controller along with detailed documentation on [software installation](/general-guides/install/), [circuit](/general-guides/electronics) and [housing](/general-guides/housing). Three common aspects of every reef-pi build. It is recommended to read through this documentation before starting with an actual build.

### Plan

reef-pi is a versatile and modular platform allowing users to customize their controller for their specific needs, tuned to their particular hardware and aquarium setup. Decide on the features you want to build first. The build process involves installing software on Raspberry Pi, soldering electronics and fabricating an enclosure (housing). None of this is hard to do, and one can definitely learn on the go, but the overall effort and time involved in this project will highly depend upon your skill level. reef-pi is aimed for beginners in computers, electronics, and reef keeping. You don't have to know software programming to build and operate reef-pi. Like most DIY projects, the reef-pi build process will require tools for soldering circuits, fabricating enclosure and keyboard/TV to configure Raspberry Pi. Due to the complexity of this project and various parts involved, error and setbacks are very common, but rarely a show stopper. Don't be dishearted, use the troubleshooting guide when needed. Users are also encouraged to ask questions in their preferred method from all the available options (email, reef2reef forum, GitHub issue or slack channel). Generally, it takes a few hours to a few weeks to build a fully functional reef-pi controller. This does not include the time spent in reading/researching or ordering the components.

### Order components

Individual reef-pi build guides provide links to purchase required components. Other than Raspberry Pi, reef-pi mainly uses Adafruit products. There are few ancillary components that are sourced from Amazon. If you are in the US, I strongly recommend using Adafruit, this project will not be a reality without them. reef-pi guides are also hosted in adafruit. The reef-pi project does not hold strong opinions on components. Users are more than welcome to use alternatives (e.g. different types of enclosures). When the software requires a specific component, we explicitly call it out. We also highly recommend salvaging older electronics. reef-pi assumes users are making judicious choices and are aware of the risks when choosing alternative components. Almost all the components can be ordered in steps. Users can get started with just a Raspberry Pi, and order components later on, incrementally working on the build. This allows iterative build process.

### Build 

During the actual build process, follow the module specific build guide. Refer to the [circuit guide](/general-guides/electronics) for wiring specific instructions. This is the most exciting part of the build. Make sure you have all required tools (e.g. soldering iron, drill kit etc) beforehand. There are few existing reef-pi build threads in reef2reef that users can refer to for getting locality specific supply chain information or alternatives.

### Test

Thoroughly test your reef-pi controller after it is built, before putting in action to safeguard your livestock. reef-pi is under active development, and like all software can contain bug, the DIY nature of reef-pi controller makes it more vulnerable to errors and inefficiencies in the due process, this is the risk that comes with its customizability. For every module, test the features you will be using and validate it with at circuit level (multimeter or equivalent) and functionally (attaching test equipment, in spare water container or tank etc).

### Deployment

Once tested, secure your circuit and all electronics component in a suitable housing. We have a [dedicated guide on building housing](/general-guides/housing). We strongly recommend fixing reef-pi housing in a stable platform. The exact options for fixing will depend on the enclosure. Most plastic enclosure based builds weigh fairly less and can be secured using Velcro strips on the wall or your aquarium cabinets. After this, your reef-pi controller is pretty much ready for use. Unless there are some hardware maintenance or upgrades, you are unlikely to touch the controller enclosure.

### Maintain

reef-pi runs on Raspberry Pi, which uses Linux operating systems. Just like reef-pi Linux is also under active development, and we recommend users to update their Linux/Raspbian installation quarterly and do a full OS upgrade (new version of Raspbian or Noobs, whatever you are going for) after every two years at least. reef-pi major releases happen every year near Thanksgiving, we strongly recommend you to consider upgrading your reef-pi software during this time. Smaller releases happen every quarter to sometimes after every two weeks (bug fixes, experimental features etc.. we are big on developing small steps and releasing frequently).
Other than updating/upgrading your build software, you may need to do some troubleshooting when you encounter any hardware failure or software bug or during the update/upgrade process of software or hardware. We have [a dedicated guide on troubleshooting](additional-documentation/troubleshooting) that covers most frequently encountered problems. For general build and reefing related help use reef2reef. We also encourage you to start a build thread in reef2reef if possible, so that others can learn from your experience as well.
