---
title: Giving the Kimiko a little upgrade
description: Upgrading the Kimiko with a new microcontroller and Cirque trackpad
date: 2022-08-16T19:29:02.266Z
tags:
  - keyboard
categories:
  - Keyboard
lastmod: 2022-08-16T20:26:37.427Z
---

Some Cirque trackpads came in, so time to give my Kimiko from [Keycapsss](https://keycapsss.com) an upgrade and while I'm at it also replace its microcontroller.

This board was using an Elite-C microcontroller, but as with all Atmega32u4, when you enable enough RGB modes and enable the OLED display, it is going to have storage problems.
So I am replacing those with a couple of [SparkFun's Pro Micro RP2040](https://www.sparkfun.com/products/18288), these use the same pinout as the Elite-C, but are missing the bottom row of pins. Since those weren't used with this keyboard anyway, that is not gonna be a problem.

The Elite-C has a power supply of 5V, since this build uses SK6812 Mini-E RGB leds we need to add a bodge wire to supply them with the raw 5V from the RP2040 instead of the usual 3.3V.

{{< gallery class="content-gallery" >}}
  {{< img src="/images/upgrade_kimiko/_DSC1869.JPG" alt="bodge wire" >}}
  {{< img src="/images/upgrade_kimiko/_DSC1871.JPG" alt="rp2040" >}}
{{< /gallery >}}

Note that I did accidently add some solder to the 3V3 pin on the microcontroller, but that one is actually not connected.

And then I added the trackpad following [the guide](https://keycapsss.com/help/cirque-trackpad) of Keycapsss.

Since the trackpad is connected to the OLED I2C pins using [@bom_tarnes](https://twitter.com/bom_tarnes) small [converter pcb](https://github.com/keyboard-magpie/minimal-fpc-i2c-pcb) and the board is now supplied with 5V, I removed Resistors R1 (for I2C), R7 and R8 (for 5V) from the trackpad.
By default the trackpad is configured for SPI and 3V.

To enable the trackpad in QMK I added to `rules.mk`:
```c
POINTING_DEVICE_ENABLE = yes
POINTING_DEVICE_DRIVER = cirque_pinnacle_i2c
```
and to `config.h`:
```c
#define CIRQUE_PINNACLE_DIAMETER_MM 40
#define POINTING_DEVICE_ROTATION_270
#define POINTING_DEVICE_GESTURES_SCROLL_ENABLE
#define CIRQUE_PINNACLE_TAP_ENABLE
```
Which also enables tap and circular scroll mode.

I also had to add the following to `rules.mk` for the RP2040:
```c
CONVERT_TO=promicro_rp2040
```

And this is the result!
{{< gallery class="content-gallery" >}}
  {{< img src="/images/upgrade_kimiko/_DSC1874.JPG" alt="result" >}}
{{< /gallery >}}