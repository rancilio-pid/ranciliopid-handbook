---
layout: default
title: Introduction to the PID system
parent: Introduction
grand_parent: EN - Manual
has_children: false
nav_order: 2
---

# Introduction to the PID system
{: .no_toc }

Contents

* TOC
{:toc}


## What is a PID control good for?

A PID controller gives considerably better control of the water temperature in your espresso machine than the standard bimetal thermostat.

A mechanical thermostat will control the water temperature in your machine within a range of about 10° Celsius, also called hysteresis. Broadly speaking, the heater in the machine's boiler will heat up to the thermostat's cut out point. The thermostat shuts off the heating and switches on the 'ready' light on the machine.

Then the boiler cools down to the thermostat's cut in point. The 'ready' light goes off and the heater reheats up to cut off again.

Between these two points, the machine is always signalling 'ready', although the water can be close to the cut out temperature, or just barely above cut in. Or pretty much anywhere in between.

Besides the exact amount of good quality beans, a good grinder and its correct coarseness setting, in an espresso shot the water temperature is one of the critical parameters. Being off by just one or two degrees Celsius can make the difference between a sour shot (too cold), a burnt one (too hot) or a 'just right', well tasting, shot of espresso. Not all coffee beans come out best at the exact same temperature, either.

One way to a reproducible temperature is called temperature surfing. It entails flushing the machine to provoke the heater coming on, and then watching the ready lamp come back on when the thermostat cuts out. That way the machine is at a defined temperature and you can prepare the shot.

Many people get annoyed by this - so were we.

The solution for small home use single boiler machines is to replace the thermostat with a PID controller that is able to hit the requested temperature within less than 1 °C. Our setup is quite capable to reach an accuracy of up to 0.1 °C. No need to hit the right time to pull a shot anymore - the right time is whenever the machine has initially warmed up.


## What can it do?

Our DIY PID has the following features:

* Control the water temperature with up to +/- 0.1 °C
* Control brewing time as well as pre infusion in the "full expansion" build
* Control brewing time based on weight
* Monitor water level in tank
* Easy control via built-in web interface
* Data monitoring via Grafana (web based) and MQTT (IoT) possible
* OTA (over the air) software updates
* PID software is open source: always free and customizable to your own needs
* Compact build, fits into most small espresso machines
* The machine's stock cabling is not modified. The machine can always be restored to its original configuration
* Active community with fast support

We always welcome feedback and feature suggestions. We encourage you to give input and move the project forward!


## List of modified espresso machines

Our system was originally developed for the Rancilio Silvia, but works just as well in other machines. We know of successful upgrades to the following machines:


 * Rancilio Silvia V1 – V4
 * Rancilio Silvia E(co) V5 & V6
 * Gaggia Classic (9303) / Classic Pro (9480) / New Classic (9403)
 * Lelit PL41 / PL42
 * La Pavoni EPL / Saeco Aroma
 * E61 single boiler (Bazzar A1 Livello, Fiorenzato Colombina)
 * E61 single boiler, dual use (Profitec Pro500)
 * Quick Mill Retro (0835) & Orione (3000)


## Differences PID Only vs. 'full expansion'

The minimal setup of our PID consists of the following components:

ID | Explanation
-|-
1 | Micro controller ESP32 (DevKitC V4)
2 | Temperature sensor TSIC 306
3 | Solid State Relais (SSR)
4 | Power supply
5 | Display (recommended, but optional)
Heizung | Heating

![Trockenaufbau](../../img/intro/einleitung/trockenaufbau.png)

There are two different levels of our system: PID only and full expansion. Over time there's been a few additional options, so the distinction is sometimes a bit less clear cut.

<!--- There would be a graphic here showing the possible levels of the PID, but it's only available in german -->


## Basic version (PID Only)

The basic version resembles a classic PID controller: the temperature sensor measures the temperature of the boiler (input) and forwards this information to the PID software running on the Micro controller (in our case ESP32). From here a control signal (output) is sent to the SSR which in turn switches the heating on and off.

By that, the PID software achieves an exact regulation of the brewing temperature while the remainder of your machine stays untouched. MQTT, Display output and control via app are also possible in the basic version.


## Extension to the basic version (PID Only+)

To give better temperature control during the brewing, you can add a sensor on to the machine's brew switch. It can then show the current brew time on the display.


## Full expansion

Here, we go one step further and transfer control over the pump and the solenoid valve to the software too. This allows for additional flexibility by controlling three time intervals via the app:

* Pre-Infusion: the pump builds up pressure (lower than brewing pressure) and the three way valve applies water onto the portafilter

* Pause: the pump pauses, but the three way valve stays open. The pressure stays and allows for the coffee in the portafilter to soak. This can help reduce channeling in the coffee puck.

* Brew time: This is the normal extraction, brewing for the amount of time predefined in the config. A longer or shorter brewing time can improve the taste of the espresso, depending on the beans used and your personal preference.

There's a distinct change to the usage of the machine: the brewing switch that was previously controlling the extraction now starts the automated process. The extraction is stopped by the controller after the predefined time, even if the switch is still engaged.

Based on our own experience and that of more than 250 users of the PID, we suggest to start with the basic version first. This gets you the biggest improvement to your coffee's taste. The full expansion allows for more flexibility, but requires a more complex modification of your machine.


## Full expansion Plus

This is where no compromises are required. You can add a scale to control the extraction time, as well as monitoring the brewing pressure using a pressure sensor.
