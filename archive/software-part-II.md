---
layout: default
title: Software Teil II
parent: DE - Handbuch1
has_children: false
nav_order: 6
---

# Software Teil II
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

In diesem Kapitel wird beschrieben wie der Code auf den Mikrocontroller (NodeMCU) geladen wird. Damit könnt ihr loslegen, sobald ihr den Mikrocontroller zur Hand habt (weitere Teile werden nicht hierfür nicht benötigt). Für einen Test sollte dann zumindest der Temperatursensor angeschlossen werden.

## userConfig.h
In dem rancilio-pid/rancilio-pid Ordner befindet sich eine für euch wichtige Datei: 
* userConfig_sample.h

Die userConfig_sample.h muss in userConfig.h umbenannt werden und mit euren Werten anpasste werden. 
Alle wichtigen Einstellungen werden für eure PID in dieser Datei vorgenommen, diese werden nun gleich genauer erläutert.
Bei einem Update auf eine neuere Version bitte unbedingt die neuste userConfig_sample.h nehmen und mit euren Werten anpassen.
Wenn Ihr das nicht tut, kann dies zu unspezifischen, nicht erwünschten Verhalten an der Maschine kommen: Display hängt, PID geht nicht und weitere


## Die Parameter in der userConfig.h

Die userConfig.h ist in mehrere Abschnitte unterteilt. Die wir nun nach und nach euch vorstellen werden. 

### List of supported machines

Die Aufzählung MACHINE enthält alle bislang unterstützen Maschinen.
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
Hier werden alle Display relevanten Einstellungen vorgenommen. 
```
#define DISPLAY 2                  // 0 = deactivated, 1 = SH1106 (e.g. 1.3 "128x64), 2 = SSD1306 (e.g. 0.96" 128x64)
#define OLED_I2C 0x3C		           // I2C address for OLED, 0x3C by default
#define DISPLAYTEMPLATE 3          // 1 = Standard Display Template, 2 = Minimal Template, 3 = only Temperatur, 4 = Scale Template, 20 = vertical Display see git Handbook for further information
#define DISPLAYROTATE U8G2_R0      // rotate display clockwise: U8G2_R0 = no rotation; U8G2_R1 = 90°; U8G2_R2 = 180°; U8G2_R3 = 270°
#define SHOTTIMER 1                // 0 = deactivated, 1 = activated 2 = with scale
#define HEATINGLOGO 0              // 0 = deactivated, 1 = Rancilio, 2 = Gaggia 
#define OFFLINEGLOGO 1             // 0 = deactivated, 1 = activated
#define BREWSWITCHDELAY 3000       // time in ms
#define LANGUAGE 1                 // LANGUAGE = 0 (DE), LANGUAGE = 1 (EN), LANGUAGE = 2 (ES)
```
DISPLAY definiert den Displaytyp. 

OLED_I2C gibt die I2C Adresse an, hier muss in der Regel nichts angepasst werden.  

DISPLAYTEMPLATE definiert das Template was ihr verwenden möchtet, siehe [Displayausgabe](https://manual.rancilio-pid.de/de/customization/Display.html).

DISPLAYROTATE lässt das Display rotieren. Beim Hochformat muss ein entsprechendes vertikale Displaytemplate (20) verwendet werden.

SHOTTIMER (1) lässt euch den Shottimer aktivieren, bei der Verwendung einer Waage kann (2) ausgewählt werden, um auch das Gewicht zu sehen.

HEATINGLOGO zeigt euch bis kurz vor Erreichen der Solltemperatur ein entsprechendes Logo anzeigen, siehe [Displayausgabe](https://manual.rancilio-pid.de/de/customization/Display.html).

OFFLINEGLOGO zeigt euch beim deaktivieren der PID via Blynk ein Logo an, siehe [Displayausgabe](https://manual.rancilio-pid.de/de/customization/Display.html).

BREWSWITCHDELAY ermöglicht euch einzustellen, wie lange die letzte Dauer beim Bezug im Display angezeigt werden soll.

LANGUAGE erlaubt es die Sprache für Displayausgaben auszuwählen.  


### Offline mode
Hier wird definiert, wie die PID sich im Offline Betrieb verhalten soll. 
```
#define OFFLINEMODUS 0             // 0 = Blynk and Wifi are used, 1 = offline mode (only preconfigured values in code are used!)
#define FALLBACK 1                 // 1 = fallback to values stored in eeprom, 0 = deactivated
#define GRAFANA 1                  // 1 = grafana visualisation (access required), 0 = off (default)
```
OFFLINEMODUS: Mit (0) wird eure PID mit Blynk und WlAN arbeiten. Bei (1) bleibt die PID offline. Daher werden alle vordefinierten PID Werte aus der userConfig.h genommen. 

FALLBACK gibt euch die Möglichkeit, dass die PID die letzten im EEPROM gespeicherten Werte nimmt, falls kein WLAN vorhanden ist. Das kann euch helfen, wenn die Maschine im Büro oder im Bereich ohne WLAN steht. Dann kann die Maschine auf den Hotspot des Handy eingestellt sein und bei Bedarf stellt man die Werte per Hotspot und Blynk ein und wenn kein WLAN vorhanden ist, nimmt die Maschine die letzten Werte. Diese werden bei jeder erfolgreichen Verbindung mit Blynk beim Start der Maschine gespeichert. 

GRAFANA aktiviert die Visualisierung mittels Grafana, diese muss in Blynk noch weiter definiert werden. 
## PID & Hardware
Hier sind die wichtigsten Parameter für die PID/Hardware definiert,
```
#define ONLYPID 1                  // 1 = Only PID, 0 = PID and preinfusion
#define ONLYPIDSCALE 0             // 0 = off , 1= OnlyPID with Scale
#define BREWMODE 1                 // 1 = NORMAL preinfusion ; 2 = Scale with weight
#define BREWDETECTION 1            // 0 = off, 1 = Software (Onlypid 1), 2 = Hardware (Onlypid 0), 3 = Sensor/Hardware for Only PID 
#define COLDSTART_PID 1            // 1 = default coldstart values, 2 = custom values via blynk (expert mode activated) 
#define TRIGGERTYPE HIGH           // LOW = low trigger, HIGH = high trigger relay
// BREWDETECTION 3 configuration
#define VOLTAGESENSORTYPE HIGH 
#define PINMODEVOLTAGESENSOR INPUT // Mode INPUT_PULLUP, INPUT or INPUT_PULLDOWN_16 (Only Pin 16)
```
ONLYPID definiert, ob ihr "OnlyPID" (1) oder den "Vollausbau" mit den Relais nutzt (0).

ONLYPIDSCALE (1) erlaubt es beim OnlyPID (1) auch die Waage zu nutzen. 

BREWMODE definiert, ob ihr nur das Ventil und die Pumpe steuert (1) oder auch eine Waage verbaut habt (2). Dazu wird in der Zukunft im Handbuch noch mehr stehen.

BREWDETECTION Diese ist hier [Brüherkennung](https://manual.rancilio-pid.de/de/customization/brueherkennung.html) genauer erläutert. Knapp zusammengefasst,
definiert ihr hier, ob diese per Software (1) , Brühschalter beim Vollausbau (2) oder per Sensor bei OnlyPid (3) erkannt werden soll. 

COLDSTART_PID gibt an, ob ihr Standard Kaltstart Parameter nehmen wollt. Diese sind durchschnittliche Werte, welche für eine Rancilio und Gaggia funktionieren sollen. Wenn ihr euch selber daran probieren wollt wählt ihr (2). Dazu hier mehr zum [Kaltstart](https://manual.rancilio-pid.de/de/customization/pid-werte.html#kaltstart)

TRIGGERTYPE HIGH es gibt LOW UND HIGH Trigger für das Ventil/Pumpe. Dies wird hier definiert.

VOLTAGESENSORTYPE und PINMODEVOLTAGESENSOR ist für die Konfiguration vom Voltagesensor hier dazu mehr: [Brüherkennung bei Only PID](
https://manual.rancilio-pid.de/de/customization/brueherkennung.html#sensor-zur-brüherkennung-bei-only-pid

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

## Weight SCALE
```
#define WEIGHTSETPOINT 30          // Gramm 
```
Hier wird mit WEIGHTSETPOINT das Sollgewicht für die Waage definiert.



##  Wifi 
```
#define HOSTNAME "rancilio"
#define D_SSID "myssid"
#define PASS "mypass"
#define MAXWIFIRECONNECTS 5        // maximum number of reconnection attempts, use -1 to deactivate
#define WIFICINNECTIONDELAY 10000  // delay between reconnects in ms
```
HOSTNAME ist der Hostname der Maschine,
D_SSID und PASS sind die Wlan Einstellungen. 

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

## Blynk
```
#define AUTH "myauth"
#define BLYNKADDRESS "blynk.clevercoffee.de"  // blynk-server IP-Address
#define BLYNKPORT 8080             // blynk-server portver 
```

## PID - offline values
```
#define SETPOINT 95                // Temperatur setpoint
#define STEAMSETPOINT 120          // Temperatur setpoint
#define AGGKP 69                   // Kp normal
#define AGGTN 399                  // Tn
#define AGGTV 0                    // Tv

// PID coldstart
#define STARTKP 50                 // Start Kp during coldstart
#define STARTTN 150                // Start Tn during cold start

// PID - offline brewdetection values
#define AGGBKP 50                  // Kp
#define AGGBTN 0                   // Tn 
#define AGGBTV 20                  // Tv
```

## Backflush values
```
#define FILLTIME 3000              // time in ms the pump is running
#define FLUSHTIME 6000             // time in ms the 3-way valve is open -> backflush
#define MAXFLUSHCYCLES 5           // number of cycles the backflush should run, 0 = disabled
```
## Pin Layout
```
#define ONE_WIRE_BUS 2             // Temp sensor pin
#define PINBREWSWITCH 0           // 0: A0 Analog PIN ; >0 : DIGITAL PIN, ESP8266: ONLY USE PIN15 AND PIN16! 
#define pinRelayVentil 12          // Output pin for 3-way-valve
#define pinRelayPumpe 13           // Output pin for pump
#define pinRelayHeater 14          // Output pin for heater
#define PINVOLTAGESENSOR  15       //Input pin for volatage sensor
//#define OLED_RESET 16            // Output pin for dispaly reset pin
#define PINETRIGGER 16             // PIN for E-Trigger relay
#define STEAMONPIN 17              // STEAM active
#define OLED_SCL 5                 // Output pin for dispaly clock pin
#define OLED_SDA 4                 // Output pin for dispaly data pin
#define HXDATPIN 99                // weight scale PIN 
#define HXCLKPIN 99                // weight scale PIN  
#define SCREEN_WIDTH 128           // OLED display width, in pixels
#define SCREEN_HEIGHT 64           // OLED display height, in pixels  
```

## Historic (no settings)
```
#define PONE 1                     // 1 = P_ON_E (default), 0 = P_ON_M (special PID mode, other PID-parameter are needed)
#define TEMPSENSOR 2               // 2 = TSIC306 1=DS18B20
```


## Historic (no settings)
```
#if (defined(ESP8266) && ((PINBREWSWITCH != 15 && PINBREWSWITCH != 0 && PINBREWSWITCH != 16 )))
  #error("WRONG Brewswitch PIN for ESP8266, Only PIN 15 and PIN 16");  
#endif
```


#endif // _userConfig_H
```


## Code hochladen

Wenn ihr die .ino Datei öffnet, öffnet sich automatisch im zweiten Tab die userConfig.h mit den wichtigen Einstellungen. Danach auf den Pfeil klicken für den Upload auf den Microkontroller. Achtet darauf, dass Ihr den Auth-Code der Blynk-App und die WLAN-Zugangsdaten im Code der userConfig.h hinterlegt habt.

![](../img/archive/software-part-II/image-2.png)

Bitte achtet vorher drauf, dass Ihr in den Board Einstellungen den richtigen COM Port ausgewählt habt.

Diesen könnt ihr auch auch im Gerätemanager prüfen (falls ihr ihn nicht wisst):

![](../img/archive/software-part-II/34.png)

![](../img/archive/software-part-II/35.png)

## Testen

Wenn alles geklappt habt könnt ihr auf dem Serial Monitor erkennen, wie sich der Microkontroller mit Blynk verbindet.

![](../img/archive/software-part-II/36.png)

Klappt das und ist der Temperatursensor korrekt angeschlossen seht ihr am Handy in der Blynk App die Raumtemperatur.
Jetzt könnt iht nach und nach die anderen Bauteile verbinden (Relais) und weiter testen.

### OTA

Hier wird der Update **O**ver **T**he **A**ir eingestellt.

Dafür muss die Maschine eingeschalten sein und sich euer Rechner (mit Arduino) im selben WLAN Netz befinden. Dann erscheint unter Werkzeuge > Port <aktuelle Auswahl> > Netzwerkschnittstellen "Rancilio <IP-Addresse>". Wählt diesen Port aus und lädt den Code entsprechend hoch.
