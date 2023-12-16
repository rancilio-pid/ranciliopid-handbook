---
layout: default
title: FAQ
parent: DE - Handbuch
has_children: false
nav_order: 8
---

# FAQ

Frage: Auf dem Display erscheint eine „emergency stop“ Warnung ab 120°C, warum?

> Die Notabschaltung greift ab 120°C, um ein Überhitzen der Maschine durch unvorhergesehenes Reglerverhalten zu vermeiden. Ab einer Temperatur <100°C wird die Notabschaltung wieder außer Kraft gesetzt. Während des Dampfbezuges erscheint diese Meldung regelmäßig (da mehr als 120°C), hat allerdings keinen Einfluss, da der Dampf nicht über den Regler gesteuert wird.

Frage: Warum schaltet der Heizungs-SSR nicht?

> Häufig passiert es, dass der Signal des Pins nicht am + Pol sondern – Pol des SSRs angeschlossen ist. Bitte prüft, ob ihr richtig den SSR angeschlossen habt. Mit einem Messgerät kann man den Durchgang bei einem SSR nicht prüfen. Höchstens, ob die gewünschten 3,3 Volt am SSR anliegen.

Frage: Meine PID-Werte passen nicht, meine Maschine schwingt über o.ä.

> Schaut bitte zu erst in unsere PID-Wert Liste [PID-Werte](./customization/pid-werte.md) oder ab Version 3.0.1 [PID-Werte](./customization/pid-werte.md), hier sind für viele PID-Werte dokumentiert für den Kaltstart, den normalen Betrieb und für die Brüherkennung. Bei Fragen im Chat bitte genau sagen, was genau nicht passt und schickt am besten Werte aus eurem Blynk dazu. Am besten im jeweiligen Chat zu den Maschinen.

Frage: Kann ich mein Iphone oder Apple Watch nutzen um z.B. den Dampfmodus zu aktivieren.
> Ja, kannst du. Der User [@saway](https://github.com/sway) hat hierzu ein Kurzbefehl gebaut, womit du via Apple Watch oder Iphone den Steam mode aktivieren kannst. Der Link zum Kurzbefehl (muss auf dem Iphone geöffnet werden): [Kurzbefehl](https://www.icloud.com/shortcuts/ee08f4989e834fecb03d96d7f3d08425) Ihr müsst nur die IP von eurer Maschine dort eintragen. (fixe IP vorrausgesetzt)

Frage: Das Display zeigt an: "PID is disabled manually"
> Wenn du das erste mal deinen PID in Betrieb nimmst, musst du die vom ESP gehostete Webseite öffnen und die PID auf der Parameter Seite aktivieren.

Frage: Mein ESP8266 startet nicht korrekt den Access Point, um mein Wlan einzurichten. Was soll ich tun? 
> Leider kollidiert der Wifi Manager und das Display bei der Ersteinrichtung. Beim ESP32 ist dieses Problem nicht vorhanden. In Release 3.3.0 haben wir den Wifimanger für den ESP8266 entfernt. Wir empfehlen ein Update auf diese Version, dort werden die Wifi Zugangsdaten wieder in der userconfig.h fest eingetragen.
