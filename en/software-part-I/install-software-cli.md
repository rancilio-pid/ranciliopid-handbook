---
layout: default
title: Install Software (CLI)
parent: Software
grand_parent: EN - Manual
has_children: false
nav_order: 2
---


# {{ page.title }}


## Overview

This installation tutorial is meant for users that prefer the command line interface (CLI).
The following steps are only tested on Linux, but should also work on MacOS.

The following software tools are required:
* Git
* Python
* PlatformIO (via pip)


## Installation Of Git

We recommend to install git via your distribution's package manager. Usually, the package is named `git`, otherwise you can find a [list of package names here](https://pkgs.org/download/git). On MacOS, it might be fastest to use [homebrew](https://brew.sh).

Clone the project into a folder of your choise:

```
$ cd repos/
$ git clone https://github.com/rancilio-pid/clevercoffee.git
$ cd clevercoffee/
```


## Installation Of PlatformIO

Create a Python Virtual Environment:

```
$ python -m venv env
```

This command creates a Python "virtual environment" named `env`.

Activate the virtual environment:

```
$ source env/bin/activate
```

Install all requirements via `pip`:

```
(env) $ pip install -U pip
(env) $ pip install setuptools platformio
```


## Compiling and Uploading

Connect your ESP32 to your computer via USB and ensure that PlatformIO recognizes the microcontroller:

```
(env) $ platformio device list
```

The output should look like the following. The important bit is the device named `/dev/ttyUSB0`:

```
[...]
/dev/ttyUSB0
------------
Hardware ID: USB VID:PID=10C4:EA60 SER=0001 LOCATION=1-3
Description: CP2102 USB to UART Bridge Controller - CP2102 USB to UART Bridge Controller
```

> **Note**: You can list all available targets with:
> ```
> (env) $ platformio run --list-targets
> ```

Now you can compile and upload the filesystem:

```
(env) $ pio run -e esp32_usb -t uploadfs
```

Now build the firmware and upload it to the ESP32:

```
(env) $ pio run -e esp32_usb -t upload
```

The ESP32 is now prepared. To restart it, press the "Reset" button on the chip hardware itself, or just reconnect the USB cable.
