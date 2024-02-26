---
layout: default
title: Version 3.0.0 & Upgrade von 2.x
parent: Einführung
grand_parent: DE - Handbuch
has_children: false
nav_order: 3
---

# Was ist anders ab Version 3.0.0 ? 
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}


## Einführung
[![Installationsvideo](https://img.youtube.com/vi/KZPjisOEcQ4/hqdefault.jpg)](https://www.youtube.com/watch?v=KZPjisOEcQ4)

Mit der Version 3.0.0 ändern sich einige Bestandteile des Projektes grundlegend. Das Handbuch konnte noch nicht vollständig aktualisiert werden, wird aber schrittweise angepasst. Diese Übersicht fasst aber bereits die wichtigsten Änderungen zusammen.  


## Einrichtung
Der Ardunio IDE wird nicht mehr aktiv von uns unterstüzt. Wir setzen ab der 3.0.0 nun vollständig auf Platform IO und VS Code.


## Funktionen


### WiFiManager
Für die Ersteinrichtung wird ein WiFiManager benutzt. Beim ersten Start des ESP wird ein Access Point von diesem geöffnet mit dem Namen "silvia" und Passwort "CleverCoffee". Dies kann in der `userConfig.h` auch angepasst werden. Verbindet ihr euch mit dem Access Point, sollte sich bei den meisten Systemen automatisch eine Seite öffnen in mittels derer ihr ein WLAN auswählen und ein Passwort eingeben könnt, welches dann gespeichert und  automatisch beim nächsten Start für die Verbindung verwendet wird.


### Webseite
Wir haben eine eigene auf dem ESP gehostet Webseite. Im Normalfall kann die Webseite über [http://`<<HOSTNAME>>`.local](#webseite) aufgerufen werden. Den hostname findet man in `platformio.ini` unter dem Wert `upload_port` (bzw. in `userconfig.h` unter dem Wert `HOSTNAME`), bitte lest euch dazu auch den Punkt [Remote Monitoring](../software-part-I/ErsteinrichtungWLAN.md#remote-monitoring) durch. *Zu beachten*: Nur Geräte im gleichen Netzwerk können die ESP gehostete Webseite erreichen! Beispiel für die Standardkonfiguration [http://silvia.local](http://silvia.local)

Ansonsten könnt ihr die IP vom ESP in eurem Router herausfinden oder per Monitor-Befehl in PlatformIO. Es bietet sich an, dem ESP eine feste IP über den Router zu vergeben und einen festen Namen über den ihr dann die Konfigurationsseite im Browser erreichen könnt.


## Wie upgrade ich von einer älteren Version (2.x oder älter)?
Es müssen wichtige Schritte vor dem Upgraden durchgeführt werden, sonst wird euer PID nicht richtig funktionieren.
In PlatformIO (VS Code) müssen folgende Schritte erfolgen, eine USB Verbindung zum ESP ist zwingend erforderlich:

Schritt | Erklärung
:--|:--
1. Flash-Speicher löschen | `nodemcuv2_usb` -> `Platform` -> `Erase Flash`
2. Dateisystem bauen und übertragen | `nodemcuv2_usb` -> `Platform` -> `Upload Fileystem Image`
3. Firmware bauen und übertragen | `nodemcuv2_usb` -> `General` -> `Upload`

Alle drei Schritte müssen nacheinander erfolgen.
 
![Update](../../img/intro/version3/platformio_upgrade.png)
 

## Helft uns!
Habt ihr Bugs oder ähnliches gefunden, lasst es uns bitte wissen. 
