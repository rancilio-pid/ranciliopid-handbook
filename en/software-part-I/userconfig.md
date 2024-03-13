---
layout: default
title: Description of userConfig.h
parent: Software
grand_parent: EN - Manual
has_children: false
nav_order: 3
---


# Description of userConfig.h

{: .no_toc}

Contents

* TOC
{:toc}


## userConfig.h

Inside the folder `rancilio-pid/rancilio-pid`, you will find an important file:
* `userConfig_sample.h`

In this file, you can set all basic configurations, for example which Pins should be used for what on the microcontroller. Those configurations will be explained in a moment.
Rename the file `userConfig_sample.h` to `userConfig.h`.

**Note**: When updating the sourcecode to a new version of the PID project, please always also use the newest version of the `userConfig_sample.h` file and edit it with the values of your existing `userConfig.h` file. Otherwise, errors could occur while compiling the new code with the old config file, or other unspecified or unwanted behaviour of the machine could occur: the display doesn't update, the PID doesn't start, etc...


## Parameters of the userConfig.h

The `userConig.h` file is splitted into multiple parts.


### List of supported machines

`MACHINE` is a list of all currently supported types of machines.

```
enum MACHINE {
  RancilioSilvia,   // MACHINEID 0
  RancilioSilviaE,  // MACHINEID 1
  Gaggia,           // MACHINEID 2
  QuickMill         // MACHINEID 3
};
```

### MACHINEID

Enter the ID of your machine here. This parameter defines what logo is shown on the display (if connected), and for the Quick Mill also detects brewing, as well as the steam mode when `BREWDETECTION` is set to 3.

```
#define MACHINEID 0                //  see above list of supported machines
```


### DISPLAY

All relevant settings for the display are configured here.

```
#define OLED_DISPLAY 2             // 0 = deactivated, 1 = SH1106 (e.g. 1.3 "128x64), 2 = SSD1306 (e.g. 0.96" 128x64)
#define OLED_I2C 0x3C              // I2C address for OLED, 0x3C by default
#define DISPLAYTEMPLATE 1          // 1 = Standard Display Template, 2 = Minimal Template, 3 = only       Temperature, 4 = Scale Template, 20 = vertical Display see git Handbook for further information
#define DISPLAYROTATE U8G2_R2      // rotate display clockwise: U8G2_R0 = no rotation; U8G2_R1 = 90°;     U8G2_R2 = 180°; U8G2_R3 = 270°
#define SHOTTIMER 1                // 0 = deactivated, 1 = activated 2 = with scale
#define HEATINGLOGO 1              // 0 = deactivated, 1 = Rancilio, 2 = Gaggia
#define OFFLINEGLOGO 1             // 0 = deactivated, 1 = activated
#define BREWSWITCHDELAY 3000       // time in ms that the brew switch will be delayed (shot timer will    show that much longer after switching off)
#define LANGUAGE 0                 // LANGUAGE = 0 (DE), LANGUAGE = 1 (EN), LANGUAGE = 2 (ES)
#define VERBOSE 0                  // 1 = Show verbose output (serial connection), 0 = show less
```

`OLED_DISPLAY` defines the type of display connected.

`OLED_I2C` defines the I2C address, this usually doesn't have to be changed.

`DISPLAYTEMPLATE` defines the template you want to use, see [display output (german)](../../de/customization/Display.md). <!-- TODO -->

`DISPLAYROTATE` rotates the display. When using portrait mode, you'll also have to use a suitable display template (20).

`SHOTTIMER` (1) activates the shot timer, when using a scale (2) can be chosen to also see the weight.

`HEATINGLOGO` shows a logo during heat-up phase, see [display output (german)](../../de/customization/Display.md).

`OFFLINEGLOGO` shows the logo when the PID is in offline mode, see [display output (german)](../../de/customization/Display.md).

`BREWSWITCHDELAY` sets the delay of still showing the brewing timer on the display after the brewing has already stopped.

`LANGUAGE` lets you pick the language on the display.

`VERBOSE` (...)


### PID & Hardware

Here, the most important parameters for the PID hardware are defined.

```
#define ONLYPID 1                  // 1 = Only PID, 0 = PID and preinfusion
#define ONLYPIDSCALE 0             // 0 = off , 1 = OnlyPID with Scale
#define BREWMODE 1                 // 1 = Brew by time (with preinfusion); 2 = Brew by weight (from scale)
#define BREWDETECTION 0            // 0 = off, 1 = Software (Onlypid 1), 2 = Hardware (Onlypid 0), 3 =    Sensor/Hardware for Only PID
#define BREWSWITCHTYPE 1           // 1 = normal Switch, 2 = Trigger Switch
#define TRIGGERTYPE HIGH           // LOW = low trigger, HIGH = high trigger relay
#define VOLTAGESENSORTYPE HIGH     // BREWDETECTION 3 configuration
#define PINMODEVOLTAGESENSOR INPUT // Mode INPUT_PULLUP, INPUT or INPUT_PULLDOWN_16 (Only Pin 16)
#define PRESSURESENSOR 0           // 1 = pressure sensor connected to A0; PINBREWSWITCH must be set to   the connected input!
#define TEMPLED 0                  // set led pin high when brew or steam set point is within range
```

`ONLYPID` defines if you use the "OnlyPID" (1) or the "Full Expansion" with relays (0).

`ONLYPIDSCALE` (1) allows you to use the scale together with the OnlyPID.

`BREWMODE` defines if you want to control only the valve and the pump (1) or if there's also a scale built in (2). In the future, there will be more information available in the manual.

`BREWDETECTION` Defines if brewing is detected by software (1), by brew switch in the full expansion (2) or via sensor in the OnlyPID version (3). This is explained in more detail here [Brew Detection (german)](../../de/customization/brueherkennung.md) <!--eliba TODO: not yet translated-->

`TRIGGERTYPE HIGH` defines the trigger type for the valve/pump. Can be `LOW` or `HIGH`.

`VOLTAGESENSORTYPE` and `PINMODEVOLTAGESENSOR` defines the voltage sensor, see: [Brew Detection In Only PID (german)](../../de/customization/brueherkennung.md#sensor-zur-brüherkennung-bei-only-pid) <!--eliba TODO: not yet translated-->

`PRESSURESENSOR` (...)

`TEMPLED` (...)


## TOF Sensor for water level measurement

```
#define TOF 0                      // 0 = no TOF sensor connected; 1 = water level by TOF sensor
#define TOF_I2C 0x29               // I2C address of TOF sensor; 0x29 by default
#define CALIBRATION_MODE 0         // 1 = enable to obtain water level calibration values; 0 = disable    for normal PID operation; can also be done in Blynk
#define WATER_FULL 102             // value for full water tank (=100%) obtained in calibration procedure (in mm); can also be set in Blynk
#define WATER_EMPTY 205            // value for empty water tank (=0%) obtained in calibration procedure  (in mm); can also be set in Blynk
```

If you don't have a TOF sensor, you can ignore this part and set `TOF` to zero (0).


## E-Trigger

```
#define ETRIGGER 0                 // 0 = no trigger (for Rancilio except Rancilio E), 1 = trigger for    CPU of Rancilio E
#define ETRIGGERTIME 60            // seconds, time between trigger signal
#define TRIGGERRELAYTYPE HIGH      // LOW = low trigger, HIGH = high trigger relay for E-Trigger
```

The Silvia E machine has an energy saving module, this can be bypassed with a relay. This can be defined here by setting `ETRIGGER` to (1).
The corresponding Pins will be defined in [Pin Layout](#pin-layout) further below.

`ETRIGGERTIME` defines the duration between signals.

`TRIGGERRELAYTYPE` is the type of relay (`HIGH` or `LOW`).


## Weight Scale

```
#define WEIGHTSETPOINT 30          // Gramm
```

`WEIGHTSETPOINT` sets the tare of the weight.


##  WiFi

```
#define HOSTNAME "rancilio"
#define MAXWIFIRECONNECTS 5        // maximum number of reconnection attempts, use -1 to deactivate
#define WIFICINNECTIONDELAY 10000  // delay between reconnects in ms
```

`HOSTNAME` sets the name of the WiFi access point during operation of the WiFiManager.

`MAXWIFIRECONNECTS` defines how often the microcontroller should try to connect to the configured WiFi during the start of the machine. If exceeded, the machine continues in offline mode.

`WIFICONNECTIONDELAY` defines the time between WiFi reconnection attempts.


## OTA

```
#define OTA true                   // true = OTA activated, false = OTA deactivated
#define OTAHOST "rancilio"         // Name to be shown in ARUDINO IDE Port
#define OTAPASS "otapass"          // Password for OTA updates
```


## MQTT

```
#define MQTT 0                             // 0 = MQTT disabled, 1 = MQTT enabled
#define MQTT_USERNAME "mymqttuser"
#define MQTT_PASSWORD "mymqttpass"
#define MQTT_TOPIC_PREFIX "custom/Küche."  // Topic will be "<MQTT_TOPIC_PREFIX><HOSTNAME>/<READING>"
#define MQTT_SERVER_IP "XXX.XXX.XXX.XXX"   // IP address of locally installed MQTT server
#define MQTT_SERVER_PORT 1883
```


## Backflush values

```
#define MAXFLUSHCYCLES 5           // Number of cycles the backflush should run, 0 = disabled
#define FILLTIME 3000              // Time in ms the pump is running
#define FLUSHTIME 6000             // Time in ms the 3-way valve is open -> backflush
```


## Pin Layout

Starting with version 3.1.3, the Pin layout is detected automatically based on the used ESP.

The mapping for the base board is done automatically when using an ESP32. Usually, nothing must be configured by hand. Otherwise, the file `esp32devkitcv4.h` must be adapted.

ESP8266 microcontrollers are also automatically mapped to the base board.
Since there are not enough Pins on the ESP8266 to cover all possible functions, you might have to configure things manually here.
The basic settings are already configured - for setting the scale, power switch, steam switch and the TempLED, you have to pick available Pins.
This can be done in the `esp8266nodemcuv2.h` file.
