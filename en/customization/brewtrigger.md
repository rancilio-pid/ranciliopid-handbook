---
layout: default
title: Brew Switch & Brew Trigger
parent: Configuration & Customization
grand_parent: EN - Manual
has_children: false
nav_order: 8
---

# Brew Switch and Brew Trigger
{: .no_toc }

Table of Contents

* TOC
{:toc}

## Introduction

CleverCoffee supports both brew switches (which remain switched on after flipping) and brew triggers (which automatically snap back after flipping) in the "full configuration". 
Depending on the hardware installed, the configuration in `userConfig.h` must be adapted: 

```
#define FEATURE_BREWSWITCH 0                     // 0 = deactivated, 1 = activated
#define BREWSWITCH_TYPE Switch::TOGGLE           // Switch::TOGGLE or Switch::MOMENTARY (trigger)
```

### Brew head rinse with brew trigger

To rinse the brew head, e.g. after a brew, the brew trigger can be held. The pump runs as long as the trigger is held. Any configured pre-infusion and pre-infusion pause are not taken into account. 

### Rancilio Silvia: Conversion of brew switch to brew trigger

The brew switch installed in older Rancilio Silvias can easily be converted to a brew trigger. To do this, open the switch as described in the [Instructions for converting the LED switch](../hardware/led-mod.md) and insert a small spring (e.g. from a ballpoint pen) into the top of the switch. Then reassemble the switch and you're done.
