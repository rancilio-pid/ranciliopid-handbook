---
layout: default
title: ESP32
parent: Hardware
grand_parent: DE - Handbuch
has_children: false
nav_order: 6
---

{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

# ESP32 Platine 

Von unsere Platine für den ESP32 gibt es inzwischen mehrere Revisionen.
Ihr findet hier Informationen zu folgenden Revisionen: 1.2, 1.3 und 1.5  
Du den einzelnen Revisionen findet ihr hier Informationen zu Bugs, Pinbelegungen, Funktionen und mehr.

## Revision 1.5

![PCB](../../../img/pcb/esp32/pcb_esp32_rev1_5.png)

In unserem Hardware Repository findet ihr das dazu passenden KiCAD Projekt und Gerber Files:
[Minimal Rev 1.5](https://github.com/rancilio-pid/clevercoffee-hardware/releases/tag/Minimal_1.5)


### Bugs
Aktuell sind keine Bugs bekannt.

###  Anschlüsse der ESP32 Platine Rev 1.5 

Header | PIN Software | Beschriftung PCB | Belegung
-|-|-|-
HT_RL | PIN 2 | IO02 | SSR Heizung     
T_SENS | PIN 16 | IO16 | Temperatursensor
I2C | PIN 21 | SDA | Display-PIN SDA
I2C | PIN 22 | SDL | Display-PIN SCL
V_IN | - | V_IN | Netzteil (5 Volt)
PV_RL | PIN 17 | Valve | Relais Ansteuerung Magnetventil
PV_RL | PIN 27 | Pump | Relais Ansteuerung Pumpe
BPSW_SW | PIN 34 | IO34 | Bezugsschalter oder Optokopler
BPSW_SW | PIN 39 | IO39 | Powerschalter  
BPSW_SW | PIN 35 | IO35 | Dampfschalter
BPSW_SW | PIN 39 | IO39 | Heisswasserschalter (noch nicht implementiert)
S_LED | PIN 26 | IO26 | Status oder Temp LED
W_SENS | PIN 23 | IO23 | Wasserstandssensor
SCALE | PIN 25 | DAT2 | Waage DAT2
SCALE | PIN 32 | DAT | Waage DAT
SCALE | PIN 33 | CLK | Waage CLK
GPIO | PIN 1 | IO01 | Für spätere Funktionen vorgesehen zb Bezugschalter LED 
GPIO | PIN 3 | IO03 | Für spätere Funktionen vorgesehen zb Drehencoder CLK
GPIO | PIN 4 | IO04 | Für spätere Funktionen vorgesehen zb Drehencoder DT
GPIO | PIN 5 | IO05 | Für spätere Funktionen vorgesehen zb Drehencoder SW
GPIO | PIN 21 | SDA | Für spätere Funktionen vorgesehen zB Drucksensor
GPIO | PIN 22 | SCL | Für spätere Funktionen vorgesehen zB Drucksensor
GPIO | PIN 12 | IO12 | JTAG Debugger TDI
GPIO | PIN 13 | IO13 | JTAG Debugger TCK
GPIO | PIN 14 | IO14 | JTAG Debugger TMS
GPIO | PIN 15 | IO15 | JTAG Debugger TDO
GPIO | PIN 18 | IO18 | Für spätere Funktionen vorgesehen zb Dimmer ZC
GPIO | PIN 19 | IO19 | Für spätere Funktionen vorgesehen zb Dampfschalter LED 

## Bestückung und Funktion

In der folgenden Liste stehen alle benötigten Bauteile und ihre Funktion:

Beschriftung PCB | Bauteil | Funktion
-|-|-
C1 | Kondensator Elko 220 µF  | Stabilisierung Spannungsversorgung
C2 | Kondensator Keramik 100 nF | Stabilisierung Spannungsversorgung
R1 | Widerstand 220 Ω | Widerstand TEMP_LED 
R2 | Widerstand 47 kΩ | Pull down Dampfschalter
R3 | Widerstand 47 kΩ | Pull down Powerschalter
R4 | Widerstand 4,7 kΩ | Pull up i2C
R5 | Widerstand 4,7 kΩ | Pull up i2C
R6 | Widerstand 47 kΩ | Pull down/up Bezugschalter
R7 | Widerstand 47 kΩ | Pull down Heisswasserschalter
JP1 | Lötjumper | Widerstand LED überbrücken für WS1812 LED
JP3 | Lötjumper | Pull down oder Pull up für Bezugsschalter oder Optokopler 

## Revision 1.3

![PCB](../../../img/pcb/esp32/pcb_esp32_rev1_3.png)

In unserem Hardware Repository findet ihr das dazu passenden KiCAD Projekt und Gerber Files:
[Minimal Rev 1.3](https://github.com/rancilio-pid/clevercoffee-hardware/releases/tag/Minimal_1.3)

### Bugs

Fehler Optokoppler für Brüherkennung:

* Nur mit High Level Trigger Optokoppler kompatibel
* Workaround für Low Level Trigger: Pulldown Widerstand R3 nicht einlöten und je nach Software Version folgende Einstellungen wählen:  
MASTER -> "OPTOCOUPLER_TYPE" auf "LOW"  
3.3.0 und älter -> "PINMODEVOLTAGESENSOR" auf "INPUT_PULLUP" und VOLTAGESENSOR auf "LOW"

* Fehlende GPIO: IO03, IO04, IO05

###  Anschlüsse der ESP32 Platine Rev 1.3 

Header | PIN Software | PIN PCB | Belegung
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
E_TRIG | PIN 25 | IO25 | Anschluss Trigger Silvia E CPU **Bis SW Version 3.X danach "SCALE DAT2"**
S_LED | PIN 26 | IO26 | Status oder Temp LED
W_SENS | PIN 23 | IO23 | Wasserstandssensor
SCALE | PIN 32 | DAT | Waage DAT
SCALE | PIN 33 | CLK | Waage CLK
GPIO | PIN 1 | IO01 | Für spätere Funktionen vorgesehen zb Bezugschalter LED
GPIO | PIN 12 | IO12 | JTAG Debugger TDI
GPIO | PIN 13 | IO13 | JTAG Debugger TCK
GPIO | PIN 14 | IO14 | JTAG Debugger TMS
GPIO | PIN 15 | IO15 | JTAG Debugger TDO
GPIO | PIN 18 | IO18 | Für spätere Funktionen vorgesehen zb Dimmer ZC
GPIO | PIN 19 | IO19 | Für spätere Funktionen vorgesehen zb Dampfschalter LED
GPIO | PIN 36 | IO36 | Heisswasserschalter (noch nicht implementiert)

## Bestückung und Funktion

In der folgenden Liste stehen alle benötigten Bauteile und ihre Funktion:

Beschriftung PCB | Bauteil | Funktion
-|-|-
C1 | Kondensator Elko 220 µF  | Stabilisierung Spannungsversorgung
C2 | Kondensator Keramik 100 nF | Stabilisierung Spannungsversorgung
R1 | Widerstand 4,7 kΩ | Pull up i2C
R2 | Widerstand 4,7 kΩ | Pull up i2C
R3 | Widerstand 47 kΩ | Pull down Bezugschalter
R4 | Widerstand 47 kΩ | Pull down Powerschalter
R5 | Widerstand 47 kΩ | Pull down Dampfschalter
R6 | Widerstand 220 Ω | Widerstand TEMP_LED 
JP1 | Lötjumper | Widerstand LED überbrücken für WS1812 LED

## Revision 1.2

![PCB](../../../img/pcb/esp32/pcb_esp32_rev1_2.png)

In unsere Hardwarem Repository findet ihr das dazu passenden KiCAD Projekt und Gerber Files:
[Minimal Rev 1.2](https://github.com/rancilio-pid/clevercoffee-hardware/releases/tag/Minimal_1.2)

### Bugs

Fehler in der Beschriftung:
HEADER | PCB Beschriftung | Richtige Beschriftung
-|-|-
S_LED | VCC | 5V 
E_TRIG | VCC | 5V 
W_SENS | IO36 | IO23 
GPIO | IO23 | IO36 

Fehler Optokoppler für Brüherkennung:

* Nur mit High Level Trigger Optokoppler kompatibel
* Workaround für Low Level Trigger: Pulldown Widerstand R3 nicht einlöten und je nach Software Version folgende Einstellungen wählen:  
MASTER -> "OPTOCOUPLER_TYPE" auf "LOW"  
3.3.0 und älter -> "PINMODEVOLTAGESENSOR" auf "INPUT_PULLUP" und VOLTAGESENSOR auf "LOW"  

* Fehlende GPIO: IO03, IO04, IO05

###  Anschlüsse der ESP32 Platine Rev 1.2 

Header | PIN Software | PIN PCB | Belegung
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
E_TRIG | PIN 25 | IO25 | Anschluss Trigger Silvia E CPU **Bis SW Version 3.X danach "SCALE DAT2"**
S_LED | PIN 26 | IO26 | Status oder Temp LED
W_SENS | PIN 23 | IO23 | Wasserstandssensor
SCALE | PIN 32 | DAT | Waage DAT
SCALE | PIN 33 | CLK | Waage CLK
GPIO | PIN 1 | IO01 | Für spätere Funktionen vorgesehen zb Bezugschalter LED
GPIO | PIN 12 | IO12 | JTAG Debugger TDI
GPIO | PIN 13 | IO13 | JTAG Debugger TCK
GPIO | PIN 14 | IO14 | JTAG Debugger TMS
GPIO | PIN 15 | IO15 | JTAG Debugger TDO
GPIO | PIN 18 | IO18 | Für spätere Funktionen vorgesehen zb Dimmer ZC
GPIO | PIN 19 | IO19 | Für spätere Funktionen vorgesehen zb Dampfschalter LED
GPIO | PIN 36 | IO36 | Heisswasserschalter (noch nicht implementiert)

## Bestückung und Funktion

In der folgenden Liste stehen alle benötigten Bauteile und ihre Funktion:

Beschriftung PCB | Bauteil | Funktion
-|-|-
C1 | Kondensator Elko 220 µF  | Stabilisierung Spannungsversorgung
C2 | Kondensator Keramik 100 nF | Stabilisierung Spannungsversorgung
R1 | Widerstand 4,7 kΩ | Pull up i2C
R2 | Widerstand 4,7 kΩ | Pull up i2C
R3 | Widerstand 47 kΩ | Pull down Bezugschalter
R4 | Widerstand 47 kΩ | Pull down Powerschalter
R5 | Widerstand 47 kΩ | Pull down Dampfschalter
R6 | Widerstand 220 Ω | Widerstand TEMP_LED 
JP1 | Lötjumper | Widerstand für LED überbrücken für WS1812 LED

