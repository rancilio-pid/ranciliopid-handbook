---
layout: default
title: Schaltpläne
parent: Hardware
grand_parent: DE - Handbuch
has_children: false
nav_order: 2
---

# Schaltpläne
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}


## Warnhinweis

> {{ site.warning.de }}


## Einleitung

Wenn der Test erfolgreich war, kannst du beginnen deinen Einbau zu planen. Unabhängig von der gewählten Ausbaustufe musst du das Netzteil und ESP mit Strom versorgen und den Temperatursensor einbauen am Kessel. Wir zeigen dir hier am Beispiel der Rancilio Siliva wie der Umbau gelingt. Weiter Maschinen, wie z.B. die Gaggia wurde auch schon erfolgreich umgebaut.


## Rancilio

### Originaler Schaltplan 

Der erste Schaltplan zeigt den original Zustand der Silvia vor dem Umbau.

![Org Schaltplan](../../schaltplan/OrginalSchaltplanRancilio.png)


### Only PID

Der zweite Schaltplan zeigt die PID Anpassung.
Diese Version ist nur für die Temperatursteuerung verantwortlich.
Die Pumpe und das 3-Wege-Ventil werden nicht durch den Controller gesteuert.

![PID Schaltplan](../../schaltplan/OnlyPIDRancilio.png)


### Only PID+

Ein Schaltplan für Only PID+, also mit Optokoppler zur Brüherkennung liegt bisher noch nicht vor. Zusätzlich zum obigen Schaltplan ist ein Optokoppler parallel zum Bezugsschalter und dem 3/2-Wegeventil zu setzen.


### Vollausbau

Der dritte Schaltplan ist der aktuelle „Vollausbau“.
Enthalten ist die PID für die Kesseltemperatursteuerung
Zusätzlich kann auch die Brühzeit oder eine „Preinfussion“ gesteuert werden. (Vorlauf-Brühzeit, Pause, Brühzeit).
Dabei werden Pumpe und das 3-Wege-Ventil vom Controller gesteuert.

**WICHTIGER HINWEIS: Dieser Umbau darf nur am Brüh-Schalter vorgenommen werden, wenn ein Schalter ohne Lampe genommen oder die Lampe ausgebaut oder eine neue Verkabelung bzw. der LED-Umbau gewählt wird, dass mit eingebauter Lampe KEINE 3,3 Volt und 230 Volt am Schalter anliegen! Sonst liegt KEINE galavanische Trennung zwischen 3,3 Volt und 230 Volt mehr vor! Das kann unter ungünstigen Umständen gefährlich für dich oder den Microcontroller sein!**

![Vollausbau Schaltplan](../../schaltplan/VollausbauRancilio.png)



