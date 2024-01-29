---
layout: default
title: ESP32
parent: Platinen
grand_parent: DE - Handbuch
has_children: false
nav_order: 1
---

# ESP32 Platine 

Von unsere Platine für den ESP32 gibt es inzwischen mehrere Revisionen.
Ihr findet hier Informationen zu folgenden Revisionen: 1.2, 1.3 und 1.5

## Revision 1.5
## Revision 1.2 und 1.3
![PCB](../../../img/pcbesp32.png)

###  PIN Belegung vom PCB ESP32 

Header PCB | PIN Software | PIN PCB | Belegung
-|-|-|-
HT_RL | PIN 2 | IO02 | SSR Heizung     
T_SENS | PIN 16 | IO16 | Temperatursensor
I2C | PIN 21 | SDA | Display-PIN SDA
I2C | PIN 22 | SDL | Display-PIN SCL
V_IN | - | V_IN | Netzteil (5 Volt)
PV_RL | PIN 17 | Valve | Relais Ansteuerung Magnetventil
PV_RL | PIN 27 | Pump | Relais Ansteuerung Pumpe
B_SW | PIN 34 | IO34 | Bezugsschalter oder Optokopler 
S_SW | PIN 35 | IO35 | Dampfschalter
P_SW | PIN 39 | IO39 | Powerschalter 
E_TRIG | PIN 25 | IO25 | Anschluss Trigger Silvia E CPU
S_LED | PIN 26 | IO26 | Status oder Temp LED
W_SENS | PIN 23 | IO23 | Wasserstandssensor
SCALE | PIN 32 | DAT | Waage DAT
SCALE | PIN 33 | CLK | Waage CLK