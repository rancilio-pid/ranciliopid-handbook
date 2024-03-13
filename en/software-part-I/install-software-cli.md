---
layout: default
title: Install Software (CLI)
parent: Software
grand_parent: EN - Manual
has_children: false
nav_order: 2
---

# {{ page.title }}
{: .no_toc }

Contents

* TOC
{:toc}


## Overview

This installation tutorial is meant for users that prefer the command line interface (CLI).
The following steps are only tested on Linux, but should also work on MacOS.

The following software tools are required:
* Git
* Python
* PlatformIO (via pip)


## Installation Of Git

We recommend to install git via your distribution's package manager, usually, the package is named `git`. On MacOS, it might be fastest to use [homebrew](https://brew.sh).

Clone the project into a folder of your choice:

```
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

## Over The Air (OTA) Updates

Newer versions can be uploaded to the ESP32 via OTA. Make sure that settings in `platformio.ini` file in section `[env:esp32_ota]` are correct.

Also make sure there is no firewall blocking the ESP32 from connecting to your host on an unprivileged port (default: random TCP port 10000-60000). This can be set to a fixed port, see [PlatformIO docs - Authentication and upload options](https://docs.platformio.org/en/latest/platforms/espressif32.html#authentication-and-upload-options).

If the `data/` directory of the project was changed since the last time flashing the ESP32:

```
(env) $ pio run -e esp32_ota -t uploadfs
```

Compile and upload the new version:

```
(env) $ pio run -e esp32_ota -t upload
```
