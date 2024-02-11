---
layout: default
title: Software
parent: DE - Handbuch
has_children: true
nav_order: 4
---

# Software
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

In diesem Kapitel wird beschrieben wie der Code auf den Mikrocontroller (ESP) geladen wird. Damit könnt ihr loslegen, sobald ihr den Mikrocontroller zur Hand habt (weitere Teile werden hierfür noch nicht benötigt). Für einen Test sollte dann zumindest der Temperatursensor angeschlossen werden.

# userConfig.h
In Ordner rancilio-pid/rancilio-pid befindet sich eine für euch wichtige Datei: 
* userConfig_sample.h

Die userConfig_sample.h muss in userConfig.h umbenannt werden und mit euren Werten anpasste werden. 
Alle wichtigen Einstellungen werden für euren Aufbau in dieser Datei vorgenommen, diese werden nun gleich genauer erläutert.
Bei einem Update auf eine neuere Version bitte unbedingt die neuste userConfig_sample.h nehmen und erneut mit euren Werten anpassen.
Wenn Ihr das nicht tut, kann dies zu Fehler beim Kompilieren oder unspezifischen, nicht erwünschtem Verhalten an der Maschine kommen: Display hängt, PID startet nicht und weitere Probleme können auftreten. 
Die genaue Beschreibung der einzelnen Werte findet ihr im Folgenden.