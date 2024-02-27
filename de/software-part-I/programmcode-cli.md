---
layout: default
title: Software installieren (CLI)
parent: Software
grand_parent: DE - Handbuch
has_children: false
nav_order: 2
---

# {{ page.title }}
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}


## Übersicht

Diese Installationsanleitung richtet sich an Benutzer, die sich auf der Kommandozeile (CLI) wohl fühlen. Die Anleitung ist ausschließlich auf Linux getestet, sollte aber auch auf MacOS funktionieren.

Ab der Version 4 für den ESP32 bzw. für den ESP8266 (bis Version 3.1.3)  werden folgende Softwaretools benötigt:
* Git
* Python
* PlatformIO (via pip)


## Installation von git

Wir empfehlen euch git direkt über den Paketmanager eurer Distribution zu installieren. Üblicherweise heißt das Paket `git`, ansonsten findet ihr [hier eine Liste](https://pkgs.org/download/git) vieler Distributionen und des Paketnamens für Git. Auf MacOS geht der Weg via [homebrew](https://brew.sh) am schnellsten.

Klont das Projekt in einen Ordner eurer Wahl:
```
$ cd repos/
$ git clone https://github.com/rancilio-pid/clevercoffee.git
$ cd clevercoffee/
```


## Installation PlatformIO

Erstellt zuerst ein Virtual Environment mit Python:
```
$ python -m venv env
```
Dieser Befehl erstellt ein Python Virtual Environment mit dem Name `env`.

Aktiviert das virtual environment:
```
$ source env/bin/activate
```

Installiert nun alle nötigen Abhängigkeiten (requirements) via `pip`:
```
(env) $ pip install -U pip
(env) $ pip install setuptools platformio
```


## Kompilieren und Upload

Schließt euren ESP32 per USB an den Rechner/Laptop an und überprüft ob PlatformIO den Mikrocontroller erkennt:
```
(env) $ pio device list
```

Die Ausgabe sollte wie folgt aussehen. Der wichtige Teil ist das Gerät `/dev/ttyUSB0`:
```
[...]
/dev/ttyUSB0
------------
Hardware ID: USB VID:PID=10C4:EA60 SER=0001 LOCATION=1-3
Description: CP2102 USB to UART Bridge Controller - CP2102 USB to UART Bridge Controller
```

> **Hinweis**: Vor den folgenden Schritten könnt ihr euch alle verfügbaren Build-Targets anzeigen lassen:
> ```
> (env) $ pio run --list-targets
> ```

Jetzt könnt ihr das Filesystem bauen und hochladen:

```
(env) $ pio run -e esp32_usb -t uploadfs
```

Jetzt noch die Firmware bauen und auf das ESP laden:

```
(env) $ pio run -e esp32_usb -t upload
```

Das ESP ist fertig vorbereitet. Um es neu zu starten reicht es den Reset-Button zu drücken, oder das USB-Kabel aus- und wieder einzustecken.

## Over The Air (OTA) Updates

Neuere Versionen können per OTA-Funktion auf das ESP32 geladen werden. Stellt dafür sicher dass die Einstellungen in `platformio.ini` im Abschnitt `[env:esp32_ota]` korrekt sind.

Stellt auch sicher dass keine Firewall den Zugriff des ESPs auf einen unpriviligierten Port auf eurem Host blockiert (standardmäßig ein zufälliger TCP-Port 10000-60000). Dieser kann als statischer Port konfiguriert werden, siehe [PlatformIO docs - Authentication and upload options](https://docs.platformio.org/en/latest/platforms/espressif32.html#authentication-and-upload-options).

Wenn es seit dem letzten Flashen des ESPs Änderungen im `data/`-Verzeichnis des Projekts gab:

```
(env) $ pio run -e esp32_ota -t uploadfs
```

Kompilieren und Hochladen der neuen Version:

```
(env) $ pio run -e esp32_ota -t upload
```
