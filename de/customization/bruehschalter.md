---
layout: default
title: Brühschalter / Brühtrigger
parent: Konfiguration & Anpassung
grand_parent: DE - Handbuch
has_children: false
nav_order: 8
---

# Brühschalter und Brühtrigger
{: .no_toc }

Inhaltsverzeichnis

* TOC
{:toc}

## Einleitung

CleverCoffee unterstützt im "Vollausbau" sowohl Brühschalter (die nach dem Umlegen angeschaltet bleiben) und Brühtrigger (die nach dem Umlegen automatisch zurückschnappen). 
Je nach verbauter Hardware ist die Konfiguration in der `userConfig.h` anzupassen: 

```
#define FEATURE_BREWSWITCH 0                     // 0 = deactivated, 1 = activated
#define BREWSWITCH_TYPE Switch::TOGGLE           // Switch::TOGGLE or Switch::MOMENTARY (trigger)
```

### Brühkopf Spülen mit Brühtrigger

Um den Brühkopf, z.B. nach einem Bezug durchzuspülen, kann der Brühtrigger gehalten werden. Die Pumpe läuft solange der Trigger gehalten wird. Eine möglicherweise konfigurierte Präinfusion und Präinfusionspause werden nicht berücksichtigt. 

### Rancilio Silvia: Umbau Brühschalter auf Brühtrigger

Der in älteren Rancilio Silvias verbaute Brühschalter kann einfach auf einen Brühtrigger umgebaut werden. Dazu wird der Schalter wie in der [Anleitung zum LED-Umbau der Schalter](../hardware/LED_Umbau.md) beschrieben geöffnet und eine kleine Feder (z.B. aus einem Kugelschreiber) oben im Schalter eingesetzt. Anschließend den Schalter wieder zusammenbauen, fertig.
