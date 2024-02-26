---
layout: default
title: Schaltpläne
parent: Hardware
grand_parent: EN - Manual
has_children: false
nav_order: 2
---

# Schaltpläne
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Warnhinweis

> {{ site.warnhinweis }}

## Einleitung

Wenn der Test erfolgreich war, kannst du beginnen deinen Einbau zu planen. Je nach Ausbaustufe musst du nur das Netzteil und Controller mit Strom versorgen, den Temperatursensor einbauen am Kessel. Wir zeigen dir hier am Beispiel der Rancilio Siliva wie der Umbau gelingt. Weiter Maschinen, wie z.B. die Gaggia wurde auch schon erfolgreich umgebaut.

## Originaler Schaltplan

Der erste Schaltplan zeigt den original Zustand der Silvia vor dem Umbau.

![Org Schaltplan](../../img/hardware/wirings/Rancilio-Cable-Original-1.jpg)

## "PID Only"

Der zweite Schaltplan zeigt die PID Anpassung.
Diese Version ist nur für die Temperatursteuerung verantwortlich.
Die Pumpe und das 3-Wege-Ventil werden nicht durch den Controller gesteuert.

![PID Schaltplan](../../img/hardware/wirings/Screenshot-at-Dez.-11-11-16-33-1536x1168.png)

## "Vollausbau"

Der dritte Schaltplan ist der aktuelle „Vollausbau“.
Enthalten ist die PID für die Kesseltemperatursteuerung
Zusätzlich kann auch die Brühzeit oder eine „Preinfussion“ gesteuert werden. (Vorlauf-Brühzeit, Pause, Brühzeit).
Dabei werden Pumpe und das 3-Wege-Ventil vom Controller gesteuert.

![Vollausbau Schaltplan](../../img/hardware/wirings/Screenshot-at-Dez.-11-11-12-33-1536x1147.png)

## Schematische Darstellung der Ausgänge der Platine ESPresso Rev 1

![Platine Schaltplan](../../img/hardware/wirings/Rancilio-Cable-Page-4.jpg)
