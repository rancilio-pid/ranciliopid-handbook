---
layout: default
title: Arduino IDE setup
parent: Software Part I
grand_parent: EN - Manual
has_children: false
nav_order: 1
---

# Arduino IDE setup

{: .no_toc }
Contents

* TOC
{:toc}

## Installation video


In this short video we explain the installation of the Arduino IDE and also show how to install our OpenSource Rancilio-PID on the NodeMCU. Have fun!

[![installation Video](https://img.youtube.com/vi/w7vBGSVWPrw/hqdefault.jpg)](https://www.youtube.com/watch?v=w7vBGSVWPrw)

## Download

Needed to transfer the program code onto the controller.


[Link to Arduino](https://www.arduino.cc/en/Main/Software)

![Screenshot of the Arduino Website](../../img/software-part-I/arduino/1.png)

## The program code

You can download the program code from the current release.

[Link to Github Repository](https://github.com/rancilio-pid/ranciliopid/releases)

![Screenshot of the Github Website](../../img/software-part-I/arduino/2.png)

## Installation of Arduino IDE

![Arduino Installation](../../img/software-part-I/arduino/installation.gif)

Help on how to install the Arduino IDE can be found at [Arduino Website](https://www.arduino.cc/en/Guide).

After succesful installation, Arduino IDE can be started from the Start menu


## Arduino preferences

### Boards Manager URL

Before we can use NodeMCU in Arduino IDE, we have to set up an additional Boards Manager URL

You can find it under: File > Preferences

| Key | Value |
|-|-|
| Boards Manager URL | `http://arduino.esp8266.com/stable/package_esp8266com_index.json`|

<details markdown="block">
  <summary> Windows </summary>

  ![Windows Arduino Preferences](../../img/software-part-I/arduino/8.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu)](../../img/software-part-I/arduino/arduino-voreinstellungen-ubu.png)

</details>

### installing board drivers

Drivers for ESP8266 **version 2.6.3** have to be installed next.

**The ESP8266 board driver has breaking changes in version 3.0, you have to use version 2.6.3!!!**

You can find those under Tools > Board: "[\<Version\>]" > Boards Manager...

<details markdown="block">
  <summary> Windows </summary>

  ![Windows Arduino Boards Manager](../../img/software-part-I/arduino/9.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu) Boards Manager](../../img/software-part-I/arduino/arduino-boardverwalter-ubu.png)

</details>

Please install the current version

Typ \<All\> > "esp": "**esp8266** by **ESP8266 Community**"

![ESP8266 install](../../img/software-part-I/arduino/boardtreiber.gif)

The Arduino IDE setup is done now, we will continue with the libraries

## installing libraries

The easiest and safest way to install all libraries correctly is to use the [libraries from Github](https://github.com/rancilio-pid/ranciliopid/tree/master/rancilio-pid/libraries). You should have downloaded them already (see [Programmcode](#the-program-code)). Just copy the whole folder into the Arduino libraries folder


| OS | Arduino Libraries Folder |
|-|-|
| Windows | `My Documents\Arduino\libraries\` |
| OSX | `~/Documents/Arduino/libraries/` |
| Linux |`~/Arduino/libraries`|

As usual, it is recommended to get more information from the official guide: [Link](https://www.arduino.cc/en/Guide/Libraries).


## Board setup

![](../../img/software-part-I/arduino/29.png)
![](../../img/software-part-I/arduino/Bildschirmfoto-2019-07-03-um-00.01.26.png)

After all libraries have been installed, it should look like this:


![](../../img/software-part-I/arduino/31.png)

Everything is now prepared for setting up Blynk and flashing of the actual code on the NodeMCU.
