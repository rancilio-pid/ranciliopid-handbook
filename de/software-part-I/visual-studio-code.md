<!---
your comment goes here
and here
--layout: default
--title: Visual Studio Code mit PlatformIO einrichten
--parent: Software
--grand_parent: DE - Handbuch
--has_children: false
--nav_order: 2
---

#   {{ page.title }}

<details open markdown="block">
  <summary>
    Inhaltsverzeichnis
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
-->
# Einführung

[Visual Studio Code](https://code.visualstudio.com/) ist ein plattformübergreifend verfügbarer Code-Editor, der sich über zahlreiche Extensions erweitern lässt. Eines der für die Entwicklung eingebetteter Systeme hilfreichsten Extensions ist [PlatformIO](https://platformio.org/). PlatformIO ermöglicht das einfache Kompilieren und Debuggen von Code für zahlreiche Mikrocontroller und ist in seiner Handhabung deutlich komfortabler und leistungsfäher als die Arduino IDE. Gleichzeitig hat PlatformIO in Verbindung mit Visual Studio Code allerdings einen deutlich größeren Funktionsumfang, wie zum Beispiel die automatische Installation aller Abhängigkeiten (Compiler, Bibliotheken, etc.) und die gleichzeitige Unterstützung mehrerer Mikrocontroller-Typen.

## Installationsvideo

In diesem kurzen Video erklären wir die Installation von Visual Studio Code und PlatformIO und zeigen, wie CleverCoffee eingerichtet und auf dem ESP installiert wird. Die Installation erfolgt hier beispielhaft in Lubuntu, funktioniert aber analog natürlich auf jedem von Visual Studio Code unterstützten Betriebssystem.
(Einige der beschriebenen Schritte zur Konfiguration sind nicht mehr ganz aktuell, die Grundlagen stimmen aber noch.)

[![Installationsvideo](http://i3.ytimg.com/vi/OpYECpZG_FE/hqdefault.jpg)](https://www.youtube.com/watch?v=OpYECpZG_FE)

## Download und Installation

[Visual Studio Code](https://code.visualstudio.com) ist für Windows, macOS und Linux verfügbar.

Empfohlen wird die Installation mit einem der folgenden Paketmanager.

### Windows über [chocolatey](https://chocolatey.org/)

```choco install vscode```

### macOS über [homebrew](https://brew.sh)

```brew install visual-studio-code```

### Linux über [Snap](https://snapcraft.io/)

```snap install vscode```

PlatformIO kann über das Extensions-Menü installiert werden. Eine allgemeine Anleitung, wie Extensions installiert werden, ist [hier](https://code.visualstudio.com/docs/editor/extension-gallery) zu finden.

In homebrew auf macOS geht das auch direkt mit:
```brew install platformio```

## Der Programmcode

Downloads des aktuellen Programmcodes findest du auf unserer Github-Projektseite bei Releases.

[Link zum Github Repository](https://github.com/rancilio-pid/clevercoffee/releases)

## Einrichtung von Visual Studio Code und PlatformIO

Im Gegensatz zur ArduinoIDE ist es bei der Arbeit mit Visual Studio Code und PlatformIO nicht notwendig, manuell Bibliotheken zu kopieren oder den Mikrocontroller (das Board) zu installieren, für das der Code kompiliert werden soll. Die notwendigen Informationen sind bereits in der Datei `platformio.ini` voreingestellt, welche Teil des Releases `rancilio-pid` ist.

Nach dem Herunterladen des Programmcodes muss man diesen in PlatformIO in Visual Studio Code über "Open Project" unter "PIO Home" -> "Open" auswählen. Beim ersten Öffnen installiert PlatformIO an dieser Stelle alle notwendigen Abhängigkeiten und Tools, wie die benötigten Compiler und Bibliotheken für die Boards. Das Projekt öffnet sich nun in der Projektansicht von PlatformIO.

Bevor man den Programmcode nun kompilieren und auf das Board laden kann, muss erst noch die Datei `userConfig.h` erstellt werden, in der alle für dich spezifischen Optionen eingetragen werden. Alle Einstellungsmöglichkeiten auf Basis dieser Datei sind in [Beschreibung der userConfig.h](./Userconfig.md) erklärt bzw. als Kommentare innerhalb der Datei vorhanden.

Wichtiger Hinweis: 
Wenn ihr das OTA Passwort in der `userconfig` ändert, muss es auch in der `platformio.ini` eingetragen werden unter: 
`upload_flags = --auth=otapass` , `otapass` ist das Passwort

## Kompilieren und Hochladen der Software
> Wichtig: Es muss zwingend "Build Filesystem Image" und "Upload Filesystem Image" erfolgen, bei einem Node mit einer älteren Version ist am Anfang "erase flash" notwendig. Sonst wird eure Webseite vom Node nicht gehen.

Sind alle Einstellungen getroffen, wählt man in der Projektansicht von PlatformIO unter  `nodemcuv2_usb` den Befehl `Build` und kompiliert so den Programmcode. Wenn dies ohne Fehler abschließt, was man anhand der `SUCCESS`-Nachricht im Terminal unten rechts ablesen kann, kann man den Code auf das per USB angeschlossene Board laden. Dazu wählt man den Befehl `Upload`, welcher auch mit `SUCCESS` erfolgreich durchlaufen sollte.

Das Projekt nutzt eine kleine Partition um Dateien auf dem Flash abzulegen. Mit dem Befehl Build Filesystem Image und Upload Filesystem Image werden die Daten auf das Board geladen. Zuvor sollte jedoch noch der Befehl Erase Flash gestartet werden um sicherzugehen, dass sich keine alten Werte von anderen Projekten oder vorherigen Versionen der Software mehr im Flash befinden, die zu Problemen führen können.

![image](https://user-images.githubusercontent.com/1299533/193664274-e8e294b8-0a34-405f-929e-6899b6080966.png)

Wenn alle diese Schritte erfolgreich durchgelaufen sind, sollte sich euer Board bereits als WLAN-Access Point gestartet haben. Der Standard-Name ist "silvia" mit dem Passwort "CleverCoffee". Verbindet euch mit diesem um die Einstellungen für euer WLAN-Netz vorzunehmen - danach verbindet sich die Maschine beim start automatisch und ihr könnt jederzeit auf das Webinterface gelangen. Detailiertere Schritte zu Konfiguration des WLANs findet ihr [hier](ErsteinrichtungWLAN.md).

Danach kann, wenn gewünscht, auch per Over-the-Air-Update eine neue Softwareversion aufgespielt werden, also über das WLAN und ohne USB-Verbindung mit dem Computer. Dafür muss lediglich die Datei `platformio.ini` angepasst und dort der zu eurem Board und euren Einstellungen passende Hostname (oder die IP-Adresse) unter `upload_port` eingetragen werden. Ist dies geschehen, wählt ihr im PlatformIO-Menü unter `nodemcuv2_ota` den Befehl `Upload`, und die Software des Boards wird über das WLAN aktualisiert. 
<!-- Dieser Prozess ist für die ArduinoIDE kurz [hier](../software-part-II.md#ota-1) erklärt.  -->
