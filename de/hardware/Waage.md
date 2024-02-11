---
layout: default
title: Waageneinbau
parent: Hardware
grand_parent: DE - Handbuch
has_children: false
nav_order: 4
---

# Aufbau und Einbau der Waage
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einführung

Für den Vollausbau besteht die Möglichkeit der Ergänzung einer Waage für den Bezug nach Gewicht (Stopp bei Zielgewicht).
Der Grundaufbau entspricht dabei bekannter Waagen mit einer Wägezelle. Diese wird mittels eines HX711 an den Arduino angeschlossen.

## Der Hardware-Aufbau

Ihr benötigt eine Wäägezelle mit einer ausreichend genauen Auflösung (0,1gr) und ausreichend Tragkraft (also größer Gewicht Abtropfschale + Lieblingstasse).
Aktuell sind folgende Zellen die meistverbauten: [Link] (https://amzn.to/2RWJnKs)

Um die Zellen am Gehäuse zu montieren gibt es eine Adapter-Lösung zum Klemmen, und eine zum Schieben, für den 3D-Drucker. 

Anschließend verbindet ihr die Zellen mit dem HX711 und diesen mit den geeigneten freien Pins am Arduino.

Bild vom Einbau:

![Waage](../../img/IMG_20210404_133048.jpg)

## Software

Vor dem Benutzen der Waage steht die Kalibrierung. Diese wird mit dem File in der HX711-Library durchgeführt. Dazu verkabelt ihr euren Waagen-Aufbau fertig, installiert die Tropfschale und steckt den Arduino per USB an.
Anschließend startet ihr die calibration.ino und führt die Kalibrierung wie beschrieben aus (auf Serial Port mit Bautrate 57600). Haltet dazu ein Kalibriergewicht parat, bei welchem euch das Gewicht bekannt ist, und das eurer Lieblingstasse mit Shot nahe kommt.
Tragt den Kalibrierungswert dann in die brewscaleini.h ein.
Ihr müsst nun noch euer PIN-layout sowie den "Scale"-modus in der Config nach eurem Setup eintragen.

## Shot nach Zielgewicht

In Blynk habt ihr im Bereich "Vollausbau" nun die Möglichkeit, neben dem Bezug nach Zeit, auch den Bezug nach Gewicht einzustellen.
Tipp: Da der Bezug entweder beim Erreichen der Zielzeit oder dem Zielgewicht stoppt, solltet ihr je nach gewünschtem Modus den anderen Wert auf einen nicht zu erreichenden Wert einstellen.
(z.B. Zielgewicht Shot = 48 gr. -> "Brühzeit"= 99 sek.)
