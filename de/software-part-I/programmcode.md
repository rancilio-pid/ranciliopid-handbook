---
layout: default
title: Software installieren
parent: Software
grand_parent: DE - Handbuch
has_children: false
nav_order: 1
---

#   {{ page.title }}
## Übersicht
Ab der Version 4 für den ESP32 bzw. für den ESP8266 (bis Version 3.1.3)  werden folgende Softwaretools benötigt:
* Visual Studio Code
* PlatformIO (eine Extension in VS Code)
* Git
* Treiber für den ESP32 / ESP8266


## Installation Visual Studio Code & PlatformIO

Geh auf die Webseite von [VS Code](https://code.visualstudio.com/download) und lade deine entsprechende Version herunter.
Öffne VS Code.
![](../../img/softwareinstall/swinstall1.png)
Suche bei Extensions (1) nach "platformio" (2). Klicke Install (3) und PlatformIO wird installiert.

Hierbei kann unten rechts im Fenster eine Meldung zeigen, dass weitere Softwarepakete fehlen:
![](../../img/softwareinstall/swinstall2.png)

Z.B. muss Python extern installiert werden. Durch den Klick auf "Install Phyton" (1) gelangt ihr in die Dokumentation
von PlatformIO. Befolgt dort die weiteren Installtionsschritte. Klickt dann in VS Code in der Meldung "Try again" 
Am Ende zeigt euch folgende Meldung, dass PlatformIO erfolgreich installiert wurde:

![](../../img/softwareinstall/swinstall3.png)

Ihr könnt aber zum aktuellen Stand ohne git oder Github Desktop nicht unseren Code kompilieren. Falls ihr dies doch tut erhaltet ihr z.B. eine folgende Fehlermeldung:
![](../../img/softwareinstall/swinstall4.png)

Ihr könnt an dieser Stelle VS Code erst einmal schließen.

## Installtion git
Wir empfehlen euch git direkt zu installieren. Auf [git scm](https://git-scm.com/downloads) sind alle Wege beschrieben, um git alleine (ohne GUI Client) für MAC OS, Windows oder Linux zu installieren. Hier geht der Weg via [homebrew](https://brew.sh) am schnellsten.

## Treiber ESP32 / ESP 8266
Ihr benötigt ggf. einen Treiber für den ESP32 bzw. ESP8266. Ihr könnt prüfen in PlatformIO unter "Device", ob euer ESP32 / ESP8266 erkannt wird:
![](../../img/softwareinstall/swinstall7.png)

Klickt in VSCode unter auf das PlatformIO Symbol ("Ameisenkopf") (1) und wählt "Devices" (2). Hier müsste der per USB verbundene ESP32 dieser zu sehen sein:
![](../../img/softwareinstall/swinstall8.png)

Es müsste ein Gerät mit "CP2102" am usbserial-X auftauchen. Wenn dies nicht der Fall ist testet bitte nochmals einen zweites USB-Kabel (manche Kabel sind nur zum Laden geeignet).
Wenn hier immer noch kein dein ESP32 / ESP 8266 auftaucht, müsst ihr den Treiber installieren:

[Treiber ESP32](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)

Der Treiber sollte auch für den ESP8266 gehen, solange der gleiche Controller verbaut ist (CP2102).

WICHTIG! Nach der Installation muss der Rechner neugestartet werden!

## Auswahl der SW-Version für den ESP32
Nach dem Neustart vom Rechner, könnt ihr prüfen, ob ihr die Software kompilieren könnt.
Öffnet das Verzeichnis in VSCode, welches ihr in Github kopiert habt. File -> Open Folder 
In dem oberen Fall wäre dies /Documents/Github/clevercoffee

In VS Code drückt ihr im Fall von MAC Shift + CMD + P oder nutzt die Taskleiste von VS Code: View -> Command Palette
Hier geht ihr ein (1): "git: clone" 
![](../../img/softwareinstall/swinstall18.png)

Damit kopiert ihr nun das Repository des Projektes von github. Gebt nun in der oberen Eingabemaske folgende URL ein (1):
https://github.com/rancilio-pid/clevercoffee
![](../../img/softwareinstall/swinstall19.png)

Die nachfolgende Meldung sucht ihr euch das Verzeichnis aus wohin das Repository kopiert werden soll, dann fügt mit "ADD to workspace" das kopierte Repository zu eurem workspace hinzu.
Es kann eine Meldung kommen, ob ihr dem Autor innerhalb des Verzeichnis vertraut, klickt hierbei auf "YES, i trust..."
![](../../img/softwareinstall/swinstall20.png)


In VS Code drückt ihr wieder im Fall von MAC Shift + CMD + P oder nutzt die Taskleiste von VS Code: View -> Command Palette
Hier geht ihr ein (1): "git: checkout to" 
![](../../img/softwareinstall/swinstall9.png) 

Drück Return oder klickt per Maus den Befehl an und es erscheint eine Auswahlliste aller Versionen:
![](../../img/softwareinstall/swinstall10.png) 

Für den ESP32 sind nur die Versionen ab 4.X.X relevant, in dieser Version wird nicht mehr der ESP8266 unterstützt. 
Die "origin/master" ist die aktuelle Version der Entwicklung für den ESP32. 

Die Master "origin/ESP8266-master" ist die alte Entwicklungsversion für den ESP8266. Hier gibt es nur noch Bugfixes. Die aktuelle Version vom ESP8266 ist jeweils die Version mit dem Zusatz "-esp8266" z.B: "v3.1.2-esp8266"
Wählt die aktuellste Version für den ESP32 aus. Es dauert paar Sekunden und dann sollte der Code heruntergeladen sein.

##  Compilieren vorbereiten
Bevor ihr die Version kompilieren könnt müssen noch kleinere Vorbereitungen passieren. 
Geht in VS Code in den Verzeichnisbaum vom Code, öffnet den Ordner /src und benennt die "userconfig_sample.h" in "userconfig.h" um:
![](../../img/softwareinstall/swinstall12.png) 

Ihr könnt nun in dieser Datei einige Dinge zu eurer Espresso Maschine einstellen. Diese sind auch ausführlicher später im Handbuch erläutert. Wichtig sind hier vor allem "ONLYPID" und die Konfiguration für den späteren Hostnamen oder die OTA Einstellungen. Die WLAN Einrichtung von euerem Netzwerk findet später direkt auf dem ESP8266 per Access Point statt.
##  Compilieren
Nun kann der Code kompiliert werden. Hierzu sind folgende Schritte notwendig:
Drückt wieder das Symbol von PlatformIO (rechts in der Leiste). Ihr könnt später per OTA auch Daten auf den ESP32 übertragen, aber aktuell muss dieser per usb bespielt werden. Der ESP32 muss hierbei angeschlossen sein per USB Kabel.
Bei jeden Upload Schritt oder Erase auf den ESP32 kann es passieren, dass dies nicht sofort durchläuft.
WICHTIG: Haltet die Taste "Boot" auf dem ESP gedrückt (ohne PINS kurzzuschließen), dann kann ein Upload per USB durchgeführt werden (Bei OTA besteht später das Problem nicht).
![](../../img/softwareinstall/swinstall13.png) 

Bei jedem Teilschritt das "SUCESS" in der Konsole abwarten:
1. (1) Daher wählt "esp32_usb" aus.  
1. (2) "Erase flash" (Boottaste am ESP32 drücken) klicken, warten bis "SUCESS"
1. (3) "Build Filesystem Image" klicken, warten bis "SUCESS"
1. (4) "Upload FIlesystem Image", Boottaste am ESP32 (beim ESP8266 nicht notwendig) drücken bis aufsteigende Prozent zu sehen sind, warten bis "SUCESS"
1. (5) Unter dem Punkt " Genereal" "Build" klicken, warten bis "SUCESS"
1. (6) Upload klicken, Boottaste am ESP32 drücken bis aufsteigende Prozent zu sehen sind, warten bis "SUCESS"
1. (7) Monitor zum ESP32 öffnen, dann sollte folgendes zu sehen sein:

```
[00:00:02] Connect to WiFi: "silvia" 
*wm:[1] AutoConnect 
*wm:[2] Setting Hostnames:  silvia
*wm:[2] Setting WiFi hostname 
*wm:[2] ESP32 event handler enabled 
*wm:[2] Connecting as wifi client... 
*wm:[2] setSTAConfig static ip not set, skipping 
*wm:[1] Connect Wifi, ATTEMPT # 1 of 3
*wm:[1] No wifi saved, skipping 
*wm:[2] Connection result: WL_NO_SSID_AVAIL
*wm:[1] Connect Wifi, ATTEMPT # 2 of 3
```
Glückwunsch der ESP32 (oder ESP8266) ist nun mit der Software bespielt, weiter geht es mit der Einrichtung vom WLAN!

