---
layout: default
title: ESP32 SMD
parent: Platinen
grand_parent: DE - Handbuch
has_children: false
nav_order: 1
---

{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

# ESP32 SMD Platine

<p>Wir sind von reinen THT-Platinen auf kombinierte SMD/THT-Platinen umgestiegen.<br>
Widerstände und Kondensatoren werden jetzt als SMD-Komponenten eingesetzt und ermöglichen eine flexible Teilbestückung.<br>
Ihr findet hier Informationen zu folgenden Revisionen: 1.1<br>
Zu den einzelnen Revisionen findet ihr in diesem Abschnitt Informationen zu Bugs, Pinbelegungen, Funktionen und mehr.</p>

## Revision 1.1

![PCB](../../img/pcb/esp32/pcb_esp32_smd_rev1_1_front.png)
![PCB](../../img/pcb/esp32/pcb_esp32_smd_rev1_1_back.png)

In unserem Hardware Repository findet ihr das dazu passenden KiCAD Projekt und Gerber Files:
[Minimal SMD Rev 1.1](https://github.com/rancilio-pid/clevercoffee-hardware/releases/tag/Minimal_SMD_1.1)


### Bugs
Aktuell sind keine Bugs bekannt.

### Anschlüsse der ESP32 SMD Platine Rev 1.1

Header | PIN Software | Beschriftung PCB | Belegung
-|-|-|-
HT_RL | PIN 2 | OUT | SSR Heizung
T_SENS | PIN 16 | SIG | Temperatursensor
I2C | PIN 21 | SDA | Display und Drucksensor - PIN SDA
I2C | PIN 22 | SCL | Display und Drucksensor - PIN SCL
V_IN | - | 5V | Netzteil (5 Volt)
PV_RL | PIN 17 | Valve | Relais Ansteuerung Magnetventil
PV_RL | PIN 27 | Pump | Relais Ansteuerung Pumpe
BPSW_SW | PIN 34 | BREW | Bezugsschalter oder Optokoppler
BPSW_SW | PIN 39 | PWR | Powerschalter
BPSW_SW | PIN 35 | STEAM | Dampfschalter
BPSW_SW | PIN 36 | WATER | Heisswasserschalter (noch nicht implementiert)
S_LED | PIN 26 | OUT | Status oder Temp LED
W_SENS | PIN 23 | SIG | Wasserstandssensor
SCALE | PIN 25 | DAT2 | Waage DAT2
SCALE | PIN 32 | DAT | Waage DAT
SCALE | PIN 33 | CLK | Waage CLK
GPIO | PIN 1 | IO01 | Für spätere Funktionen vorgesehen zb Bezugschalter LED
GPIO | PIN 3 | IO03 | Für spätere Funktionen vorgesehen zb Drehencoder CLK
GPIO | PIN 4 | IO04 | Für spätere Funktionen vorgesehen zb Drehencoder DT
GPIO | PIN 5 | IO05 | Für spätere Funktionen vorgesehen zb Drehencoder SW
GPIO | PIN 21 | SDA | Für spätere Funktionen vorgesehen zB IO Expander
GPIO | PIN 22 | SCL | Für spätere Funktionen vorgesehen zB IO Expander
GPIO | PIN 12 | IO12 | JTAG Debugger TDI
GPIO | PIN 13 | IO13 | JTAG Debugger TCK
GPIO | PIN 14 | IO14 | JTAG Debugger TMS
GPIO | PIN 15 | IO15 | JTAG Debugger TDO
GPIO | PIN 18 | IO18 | Für spätere Funktionen vorgesehen zb Dimmer ZC
GPIO | PIN 19 | IO19 | Für spätere Funktionen vorgesehen zb Dampfschalter LED

### Bestückung und Funktion

In der folgenden Liste stehen alle benötigten Bauteile und ihre Funktion:

Beschriftung PCB | Bauteil | Funktion
-|-|-
C1 | Kondensator Elko 220 µF | Stabilisierung Spannungsversorgung
C2 | Kondensator Keramik 100 nF | Stabilisierung Spannungsversorgung
R1 | Widerstand 220 Ω | Widerstand TEMP_LED
R2 | Widerstand 47 kΩ | Pull down/up Dampfschalter
R3 | Widerstand 47 kΩ | Pull down/up Powerschalter
R4 | Widerstand 4,7 kΩ | Pull up i2C
R5 | Widerstand 4,7 kΩ | Pull up i2C
R6 | Widerstand 47 kΩ | Pull down/up Bezugschalter
R7 | Widerstand 47 kΩ | Pull down/up Heisswasserschalter
JP1 | Lötjumper | Widerstand für LED überbrücken bei Verwendung von WS1812 LED
JP2 | Lötjumper | Pull down oder Pull up für Heisswasserschalter
JP3 | Lötjumper | Pull down oder Pull up für Bezugsschalter oder Optokoppler
JP4 | Lötjumper | Pull down oder Pull up für Powerschalter
JP5 | Lötjumper | Pull down oder Pull up für Dampfschalter

### Lötjumper Einstellungen

Mit den Lötjumper lassen sich für die Schalter für Heisswasser, Bezug, Power und Dampf die Widerstände zwischen Pulldown und Pullup tauschen.
Über die Widerstände wird der Zustand des Schaltereinganges im unbetätigten Zustand definiert.
Die Standardkonfiguration sieht vor das alle Jumper auf Pulldown gelötet werden.
Bei der Verwendung eines Optokopplers für die Bezugserkennung, muss in den meisten Fällen der Lötjumper JP3 als Pullup verlötet werden.

### Änderungen

- Widerstände und Kondensatoren als SMD Bauteile 
- Pull-Widerstände für Bezug, Heißwasser, Dampf und Power als Lötjumper 