---
layout: default
title: Arduino IDE einrichten
parent: Software Teil I
grand_parent: DE - Handbuch
has_children: false
nav_order: 2
---

# Arduino IDE einrichten

{: .no_toc }
Inhaltsverzeichnis

* TOC
{:toc}

## Installationsvideo

In diesem kurzen Video erklären wir die Installation der Arduino IDE und zeigen wie unsere OpenSource Software Rancilio-PID auf dem NodeMCU installiert wird. Viel Spaß!

[![Installationsvideo](https://img.youtube.com/vi/w7vBGSVWPrw/hqdefault.jpg)](https://www.youtube.com/watch?v=w7vBGSVWPrw)

## Download

Wird benötigt, um den Code auf den Controller zu spielen.

[Link zu Arduino](https://www.arduino.cc/en/Main/Software)

![Screenshot der Arduino Homepage](../img/archive/arduino/1.png)

## Installation der Arduino IDE

![Arduino Installation](../img/archive/arduino/installation.gif)

Hinweise zur Installation befinden sich auf der [Arduino Homepage](https://www.arduino.cc/en/Guide).

Nach der erfolgreichen Installation kann Arduino über das Startmenü gestartet werden.

## Arduino Voreinstellungen

### Boardverwaltungs-URL anlegen

Wir benötigen für den Einsatz des NodeMCUs eine zusätzliche Boardverwaltungs-URL.

Diese erreicht ihr unter: Datei > Voreinstellungen

| Key | Value |
|-|-|
| Boardverwaltungs-URL | `http://arduino.esp8266.com/stable/package_esp8266com_index.json`|

<details markdown="block">
  <summary> Windows </summary>

  ![Windows Arduino Voreinstellungen](../img/archive/arduino/8.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu)](../img/archive/arduino/arduino-voreinstellungen-ubu.png)

</details>

### Boardtreiber installieren

Als nächstes müssen die ESP8266 Boardtreiber in Version **2.6.3** installiert werden.

**In der neuesten version der Boardtreiber (ab Version 3.0) gibt es breaking changes, ihr müsst Version 2.6.3 benutzen!!!**


Dies erreicht ihr unter: Werkzeuge > Board: "[\<Version\>]" > Boardverwalter...

<details markdown="block">
  <summary> Windows </summary>

  ![Windows Arduino Boardverwalter](../img/archive/arduino/9.png)

</details>

<details markdown="block">
  <summary> Linux (Ubuntu) </summary>

  ![Linux (Ubuntu) Boardverwalter](../img/archive/arduino/arduino-boardverwalter-ubu.png)

</details>

Bitte die aktuelle Version installieren.

Typ \<Alle\> > "esp": "**esp8266** by **ESP8266 Community**"

![ESP8266 installieren](../img/archive/arduino/boardtreiber.gif)

Nun ist die Arduino IDE vorbereitet. Weiter geht es mit den Bibliotheken.

## Bibliotheken installieren

Der sicherste und einfachste Weg alle Bibliotheken korrekt zu installieren, ist es, die [Bibliotheken aus Github](https://github.com/rancilio-pid/ranciliopid/tree/master/rancilio-pid/libraries) zu nehmen. Diese solltet ihr bereits heruntergeladen haben (siehe [Programmcode](#der-programmcode)). Kopiert die kompletten Ordner einfach in den Arduino Libraries Ordner zu kopieren:<!-- markdown-link-check-disable-line -->

| OS | Arduino Libraries Ordner |
|-|-|
| Windows | `My Documents\Arduino\libraries\` |
| OSX | `~/Documents/Arduino/libraries/` |
| Linux |`~/Arduino/libraries`|

Wie immer ist es empfehlenswert beim offiziellen Guide mehr Infos einzuholen: [Link](https://www.arduino.cc/en/Guide/Libraries).

### Bibliotheken manuell installieren

Alternativ müssen folgende Libraries per Hand installiert werden:

* Blynk
* TimeLib
* WidgetRTC
* U8x8lib
* OneWire
* DallasTemperature
* PID_v1.h
* Adafruit VL53L0X

Die Installation der einzelnen Bibliotheken erfolgt wieder über die Verwaltung in Arduino IDE:

![Bibliotheken verwalten](../img/archive/arduino/12.png)

<details markdown="block">
  <summary> OneWire </summary>

  ![](../img/archive/arduino/13.png)
</details>

<details markdown="block">
  <summary>
    DallasTemperature
  </summary>

![](../img/archive/arduino/14.png)
</details>

<details markdown="block">
  <summary> U8x8lib </summary>

  1. Geht auf [https://github.com/olikraus/u8g2](https://github.com/olikraus/u8g2)
  1. Code > Download Zip
  ![](../img/archive/arduino/15.png)
  1. Legt die Dateien im [Arduino Libraries Ordner](#bibliotheken-installieren) ab
  1. Erstellen einen Ordner: `U8x8lib`
  1. Den Inhalt aus dem ZIP File Ordner: u8g2-master.zip\u8g2-master\cppsrc  UND csrc in den neu erstellten Ordner kopieren (ja, es sind eine ganze Menge Dateien :))
  ![](../img/archive/arduino/16.png)
  ![](../img/archive/arduino/17.png)
</details>

<details markdown="block">
  <summary> PID_v1.h </summary>

  1. Geht auf [https://github.com/br3ttb/Arduino-PID-Library](https://github.com/br3ttb/Arduino-PID-Library)
  1. Code > Download Zip  
  ![](../img/archive/arduino/arduino-pid-lib.png)
  1. Legt die Dateien im [Arduino Libraries Ordner](#bibliotheken-installieren) ab
  1. Erstellen einen Ordner: `PID_v1`
  1. Die vier Dateien aus dem ZIP File kopieren und in den neuen Ordner einfügen:
  ![](../img/archive/arduino/19.png)
  ![](../img/archive/arduino/20.png)
</details>

<details markdown="block">
  <summary> Blynk </summary>

  1. Geht auf [https://www.blynk.cc/getting-started/](https://www.blynk.cc/getting-started/)
  ![](../img/archive/arduino/21.png)
  1. Geht auf [https://github.com/blynkkk/blynk-library/releases/tag/v0.5.4](https://github.com/blynkkk/blynk-library/releases/tag/v0.5.4)
  ![](../img/archive/arduino/22.png)
  ![](../img/archive/arduino/23.png)
  ![](../img/archive/arduino/25.png)
  ![](../img/archive/arduino/26.png)
  1. Wechseln in den [Arduino Libraries Ordner](#bibliotheken-installieren)
  ![](../img/archive/arduino/27.png)
  ![](../img/archive/arduino/28.png)
</details>

## Board einstellen

![](../img/archive/arduino/29.png)
![](../img/archive/arduino/Bildschirmfoto-2019-07-03-um-00.01.26.png)

Wenn alle Bibliotheken installiert sind, müsste es wie folgt aussehen:

![](../img/archive/arduino/31.png)

Somit ist alles nun für das Einrichten von Blynk und das Flashen von dem Code vorbereitet. Dann kann der erste Test beginnen.
