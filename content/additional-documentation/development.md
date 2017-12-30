---
author: "Ranjib Dey"
date: 2017-07-20
linktitle: devenvironment
title: Development environment
highlight: true
weight: 7
keywords:
- reef-pi
- reef tank
- controller
- raspberry pi
- coral
---

reef-pi is written in [go](https://golang.org/) and [react](https://facebook.github.io/react/). This guide will walk through the steps involved in
setting up go and nodejs (required for react) development environment, alongside
reef-pi. This guide assume OSX or Linux as the development platform.

### Setup go

reef-pi is built and tested with latest go. At the time of writing the guide, the latest
version of go is 1.8.1. reef-pi should work with any version of go above 1.5.

Use any one of the three ways to install go:

1. I recommend using the official [go installation guide](https://golang.org/doc/install) to install go in your development machine.

2. In most cases, for linux based development environment use distribution specific package managers (dnf or apt or yum) to download
latest go. Ubuntu linux specific go installation instruction can be found [here](https://github.com/golang/go/wiki/Ubuntu)

3. For OSX users, if you have homebrew installed, it is as simple as

```
brew install go
```

Irrespective of how you install go, make sure you set GOPATH environment variable. I recommend setting GOPATH environment variable inside your home
directory, in a dedicated sub directory: `/home/ranjib/gospace`. Declare GOPATH in your .bashrc or .bash_profile so that it persist
between sessions.

```sh
export GOPATH=/home/user/gospace
```

### Setup nodejs

All the User Interface components in reef-pi is written using [react](https://facebook.github.io/react/), which requires nodejs
for development. Follow the official nodejs [installation guide](https://docs.npmjs.com/getting-started/installing-node) to install nodejs in your development machine.
reef-pi requires nodejs version 7.0 or above.

For OSX users, if you have homebrew installed, this is as simple as

```
brew install node
```

This will install both nodejs and npm, the package manager for nodejs based librariea. reef-pi uses npm to manage nodejs libraries.


### Building and running reef-pi on developer machine

Once go and nodejs is setup, you are ready to start with reef-pi code base itself.

- Copy reef-pi code from github to your $GOPATH

```
git clone https://github.com/ranjin/reef-pi.git $GOPATH/src/github.com/ranjib/reef-pi
```

To keep reef-pi simple and reliable, I have not yet integrated any go package manager. Hence the example shows cloning reef-pi repository
inside the $GOPATH, without this go-get command will fail. All following commands & instructions assume you are working from the reef-pi
repository itself, i.e.

```
cd $GOPATH/src/github.com/ranjib/reef-pi
```

- Downnloading dependencies: Now that reef-pi code base is cloned, you can start downloading all the dependencies. To install all go libraries use

```
make go-get
```

Install all reef-pi UI or reactjs dependencies

```
npm install
```

This will install reactjs, webpack and ancillary package used by reef-ui

- Build reef-pi binary
Make reef-pi binary
```
make
```
Compile all jsx code to javascript
```
./node_modules/.bin/webpack -d
```

At this point both reef-pi binary and the javascript components are built to run reef-pi on the development machine. All we need now is to start reef-pi in dev_mode (so that all device drivers calls are ignored).

```
DEV_MODE=1 ./bin/reef-pi
```
Head over to your browser [http://localhost:8080/](http://localhost:8080) to see the reef-pi in action.


### Running reef-pi on a raspberry pi

It is likely you would want to test out a new feature on a physical raspberry pi once you have writtend the code for a new feature. The default make target will create development machine specific binary. For Raspberry Pi, reef-pi needs to be compiled for ARM 6 (raspberry pi zero) or ARM7 architecture. reef-pi's [Makefile](https://github.com/ranjib/reef-pi/blob/master/Makefile)
has predefined target for this. To create raspberry pi 3 or 2 specific binary, run

```
make pi
```

To create pi zero specific binary, run

```
make pi-zero
```

Next generate a debian package for the pi zero. This will package the javascript front end, along side systemd unit files and a stock configuration file. 

```
make deb
```

This debian package can be copied over to a Raspberry Pi computer and run there.

```
scp reef-pi-x.x.x.deb pi@<IP>:.
```

To install the new package on pi zero, run
```
sudo dpkg -i reef-pi-x.x.x.deb
```

This will install reef-pi binary, create the necessary directory structure, install and start reef-pi systemd service. You can check status of reef-pi service with
```
sudo systemctl status reef-pi.service
```

Note, if theres an already installed reef-pi, you have to remove it first. To do so, use the following command:

```
sudo apt-get remove -y --purge reef-pi
```
