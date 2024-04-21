---
layout: default
title: FAQ
parent: EN - Manual
has_children: false
nav_order: 7
---

# FAQ

Question: The warning „emergency stop“ appears on the display at 120°C, why?

> The emergency shutdown kicks in at 120 °C in order to prevent overheating of the machine, which caused by onforseen behaviour of the software or hardware. After the temperature has dropped below 100 °C, the PID will resume normal operation. When in steam mode, this message will apear regulary (temp. above 120 °C), but doesn't influence the function of the machine since steam is not controlled by the PID.  


Question: why does the heating SSR not function properly?

> A common mistake is that the signal pin is not connected to "+", but to the "-" connector of the SSR. Please double check if you have connected the SSR correctly


Question: My PID values don't seem to work, e.g. the temperature overshoots

> Please have a look at our PID-value list [PID-values](../de/customization/pid-werte.md), where many working values are listed for cold-start, normal operation and brew-detection. In case you want to ask for help in the chat, please explain the exact problem (best would be to also send the values from Blynk).

Question: My microcontroller seems to detect brews and brew stops, and randomly switches between those two at frequent intervals. Why?

> Dependig of the level of expansion you chose (PID only to full expansion), you might need the resistor `R6` for your build. Also check that you solder-bridged `JP2` correctly on the back side of the PCB base board ([see JP2](./pcb/ESP32.md#placement-and-function) starting with PCB version 1.5).
