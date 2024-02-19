---
layout: default
title: Beschreibung der userConfig.h
parent: Software
grand_parent: DE - Handbuch
has_children: false
nav_order: 3
---


# Beschreibung der userConfig.h
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}


## userConfig.h
In dem rancilio-pid/rancilio-pid Ordner befindet sich eine für euch wichtige Datei: 
* userConfig_sample.h

Die userConfig_sample.h muss in userConfig.h umbenannt werden und mit euren Werten anpasste werden. 
Grundlegende Einstellungen wie genutzte Pins werden in dieser Datei vorgenommen, diese werden nun gleich genauer erläutert.
Bei einem Update auf eine neuere Version bitte unbedingt die neuste userConfig_sample.h nehmen und mit euren Werten anpassen.

## Die Parameter in der userConfig.h

Die userConfig.h ist in mehrere Abschnitte unterteilt.

### List of supported machines

Die Aufzählung MACHINE enthält alle bislang unterstützen Maschinentypen.
```
enum MACHINE {
  RancilioSilvia,   // MACHINEID 0
  RancilioSilviaE,  // MACHINEID 1
  Gaggia,           // MACHINEID 2
  QuickMill         // MACHINEID 3
};
```

### MACHINEID
```
#define MACHINEID 0                //  see above list of supported machines
```
Hier müsst ihr die ID eurer Maschine eintragen. Dieser Parameter steuert die Logodarstellung auf dem Display (wenn angeschlossen) und bei der Quick Mill die Erkennung des Brühvorgangs und den Dampfmodus bei BREWDETECTION 3.

### DISPLAY
Hier werden alle für das Display relevanten Einstellungen vorgenommen. 

```
#define OLED_DISPLAY 2             // 0 = deactivated, 1 = SH1106 (e.g. 1.3 "128x64), 2 = SSD1306 (e.g. 0.96" 128x64)
#define OLED_I2C 0x3C              // I2C address for OLED, 0x3C by default
#define DISPLAYTEMPLATE 1          // 1 = Standard Display Template, 2 = Minimal Template, 3 = only Temperature, 4 = Scale Template, 20 = vertical Display see git Handbook for further information
#define DISPLAYROTATE U8G2_R2      // rotate display clockwise: U8G2_R0 = no rotation; U8G2_R1 = 90°; U8G2_R2 = 180°; U8G2_R3 = 270°
#define SHOTTIMER 1                // 0 = deactivated, 1 = activated 2 = with scale
#define HEATINGLOGO 1              // 0 = deactivated, 1 = Rancilio, 2 = Gaggia
#define OFFLINEGLOGO 1             // 0 = deactivated, 1 = activated
#define BREWSWITCHDELAY 3000       // time in ms that the brew switch will be delayed (shot timer will show that much longer after switching off)
#define LANGUAGE 0                 // LANGUAGE = 0 (DE), LANGUAGE = 1 (EN), LANGUAGE = 2 (ES)
#define VERBOSE 0                  // 1 = Show verbose output (serial connection), 0 = show less
```
OLED_DISPLAY definiert den Displaytyp. 

OLED_I2C gibt die I2C Adresse an, hier muss in der Regel nichts angepasst werden.  

DISPLAYTEMPLATE definiert das Template was ihr verwenden möchtet, siehe [Displayausgabe](https://manual.rancilio-pid.de/de/customization/Display.html).

DISPLAYROTATE lässt das Display rotieren. Beim Hochformat muss ein entsprechendes vertikale Displaytemplate (20) verwendet werden.

SHOTTIMER (1) aktiviert den Shot Timer, bei der Verwendung einer Waage kann (2) ausgewählt werden, um auch das Gewicht zu sehen.

HEATINGLOGO zeigt euch bis kurz vor Erreichen der Solltemperatur ein entsprechendes Logo an, siehe [Displayausgabe](https://manual.rancilio-pid.de/de/customization/Display.html).

OFFLINEGLOGO zeigt euch beim deaktivieren des PIDs ein Logo an, siehe [Displayausgabe](https://manual.rancilio-pid.de/de/customization/Display.html).

BREWSWITCHDELAY ermöglicht euch einzustellen, wie lange die Dauer des Bezugs im Display noch angezeigt werden soll, nachdem der Brühvorgang bereits beendet ist.

LANGUAGE erlaubt es die Sprache für Displayausgaben auszuwählen.  

VERBOSE (...)

## PID & Hardware
Hier sind die wichtigsten Parameter für die PID/Hardware definiert,

```
#define ONLYPID 1                  // 1 = Only PID, 0 = PID and preinfusion
#define ONLYPIDSCALE 0             // 0 = off , 1 = OnlyPID with Scale
#define BREWMODE 1                 // 1 = Brew by time (with preinfusion); 2 = Brew by weight (from scale)
#define BREWDETECTION 0            // 0 = off, 1 = Software (Onlypid 1), 2 = Hardware (Onlypid 0), 3 = Sensor/Hardware for Only PID
#define BREWSWITCHTYPE 1           // 1 = normal Switch, 2 = Trigger Switch
#define TRIGGERTYPE HIGH           // LOW = low trigger, HIGH = high trigger relay
#define VOLTAGESENSORTYPE HIGH     // BREWDETECTION 3 configuration
#define PINMODEVOLTAGESENSOR INPUT // Mode INPUT_PULLUP, INPUT or INPUT_PULLDOWN_16 (Only Pin 16)
#define PRESSURESENSOR 0           // 1 = pressure sensor connected to A0; PINBREWSWITCH must be set to the connected input!
#define TEMPLED 0                  // set led pin high when brew or steam set point is within range
```
ONLYPID definiert, ob ihr "OnlyPID" (1) oder den "Vollausbau" mit den Relais nutzt (0).

ONLYPIDSCALE (1) erlaubt es beim OnlyPID (1) auch die Waage zu nutzen. 

BREWMODE definiert, ob ihr nur das Ventil und die Pumpe steuert (1) oder auch eine Waage verbaut habt (2). Dazu wird in der Zukunft im Handbuch noch mehr stehen.

BREWDETECTION Diese ist hier [Brüherkennung](https://manual.rancilio-pid.de/de/customization/brueherkennung.html) genauer erläutert. Knapp zusammengefasst,
definiert ihr hier, ob diese per Software (1) , Brühschalter beim Vollausbau (2) oder per Sensor bei OnlyPid (3) erkannt werden soll. 

TRIGGERTYPE HIGH es gibt LOW UND HIGH Trigger für das Ventil/Pumpe. Dies wird hier definiert.

VOLTAGESENSORTYPE und PINMODEVOLTAGESENSOR ist für die Konfiguration vom Voltagesensor hier dazu mehr: [Brüherkennung bei Only PID](
https://manual.rancilio-pid.de/de/customization/brueherkennung.html#sensor-zur-brüherkennung-bei-only-pid

PRESSURESENSOR (...)

TEMPLED (...)

## TOF sensor for water level

```
#define TOF 0                      // 0 = no TOF sensor connected; 1 = water level by TOF sensor
#define TOF_I2C 0x29               // I2C address of TOF sensor; 0x29 by default
#define CALIBRATION_MODE 0         // 1 = enable to obtain water level calibration values; 0 = disable for normal PID operation; can also be done in Blynk
#define WATER_FULL 102             // value for full water tank (=100%) obtained in calibration procedure (in mm); can also be set in Blynk
#define WATER_EMPTY 205            // value for empty water tank (=0%) obtained in calibration procedure (in mm); can also be set in Blynk
```
Habt ihr keinen TOF Sensor, könnt ihr diesen Teil ignorieren und TOF (0) einstellen.  


## E-Trigger
```
#define ETRIGGER 0                 // 0 = no trigger (for Rancilio except Rancilio E), 1 = trigger for CPU of Rancilio E
#define ETRIGGERTIME 60            // seconds, time between trigger signal
#define TRIGGERRELAYTYPE HIGH      // LOW = low trigger, HIGH = high trigger relay for E-Trigger
```
Die Silvia E hat ein Energiesparmodul, dieses kann überbrückt werden mit einem Relais. Dieses kann hier definiert werden, wenn ETRIGGER (1) gewählt wird.
Der zugehörige PIN wird später definiert, im Abschnitt PIN Layout.

ETRIGGERTIME ist die Zeitdauer zwischen den Signalen.

TRIGGERRELAYTYPE ist der Relaistyp (High oder LOW).

## Weight Scale
```
#define WEIGHTSETPOINT 30          // Gramm 
```
Hier wird mit WEIGHTSETPOINT das Sollgewicht für die Waage definiert.

##  Wifi 
```
#define HOSTNAME "rancilio"
#define MAXWIFIRECONNECTS 5        // maximum number of reconnection attempts, use -1 to deactivate
#define WIFICINNECTIONDELAY 10000  // delay between reconnects in ms
```
HOSTNAME ist der Hostname der Maschine,

MAXWIFIRECONNECTS definiert wie viele Reconnect gemacht werden, bis der Fallback aktiviert wird (bei Start der Maschine) oder bis der Offline Modus aktiviert wird (nach dem erfolgreichen Start)

WIFICINNECTIONDELAY ist die Zeitspanne bis der nächste Reconnect probiert wird. 

## OTA
```
#define OTA true                   // true = OTA activated, false = OTA deactivated
#define OTAHOST "rancilio"         // Name to be shown in ARUDINO IDE Port
#define OTAPASS "otapass"          // Password for OTA updtates
```

## MQTT

```
#define MQTT 0                     // 1 = MQTT enabled, 0 = MQTT disabled
#define MQTT_USERNAME "mymqttuser"
#define MQTT_PASSWORD "mymqttpass"
#define MQTT_TOPIC_PREFIX "custom/Küche."  // topic will be "<MQTT_TOPIC_PREFIX><HOSTNAME>/<READING>"
#define MQTT_SERVER_IP "XXX.XXX.XXX.XXX"  // IP-Address of locally installed mqtt server
#define MQTT_SERVER_PORT 1883    
```

## Backflush values

```
#define FILLTIME 3000              // time in ms the pump is running
#define FLUSHTIME 6000             // time in ms the 3-way valve is open -> backflush
#define MAXFLUSHCYCLES 5           // number of cycles the backflush should run, 0 = disabled
```

## Pin Layout

Das Pin Layout wird ab Version 3.1.3 automatisch aufgrund des verwendeten ESPs ausgewählt.

Für den ESP32 wird automatisch das zu unserem PCB passende Mapping vorgenommen. Grundsätzlich müssen hier keine Änderungen vorgenommen werden.
Wenn doch muss das in der "esp32devkitcv4.h" gemacht werden.

Für den ESP8266 wird automatisch das zu unserem PCB passende Mapping vorgenommen.
Da der ESP8266 aber grundsätzlich nicht genügend Anschlüsse hat für alle Funktionen, müsst ihr hier möglicherweise Hand an legen.
Die Grundfunktionen sind schon fertig belegt, für die Waage, Powerswitch, Steamswitch und TempLED müsst ihr die Pins erst noch konfigurieren.
Das ist in der "esp8266nodemcuv2.h" zu erledigen.
