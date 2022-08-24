---
title: Cocot46plus build notes
description: Notes on my Cocot46plus build
date: 2022-08-24T21:24:44.976Z
tags:
  - keyboard
categories:
  - Keyboard
lastmod: 2022-08-24T23:37:53.046Z
---

# {{< img src="/images/cocot46plus/_DSC2015.JPG" alt="cocot46plus" >}}

{{< toc "Contents:" >}}

## Cocot46plus

I recently received my [Cocot46plus](https://aki27.booth.pm/items/3879034) kit, which I got via Charly who lives in Japan (many thanks!), which is a Japanese board designed by [aki27](https://twitter.com/aki27kbd) with 46 keys in a Corne-like layout, trackball, OLED indicating layer and trackball status, RGB leds, and rotary encoder, intended for a normal 5V Atmega32u4 Pro Micro.
This is the first unibody I built and it seemed very interesting because its form, the dedicated mouse buttons, encoder, and the same 34mm trackball which is also used in the Charybdis.

## Parts

{{< gallery class="content-gallery" >}}
    {{< img src="/images/cocot46plus/_DSC1876.JPG" alt="kit content" >}}
    {{< img src="/images/cocot46plus/_DSC1880.JPG" alt="PCB front" >}}
    {{< img src="/images/cocot46plus/_DSC1881.JPG" alt="PCB back" >}}
    {{< img src="/images/cocot46plus/_DSC1882.JPG" alt="Switch plate" >}}
    {{< img src="/images/cocot46plus/_DSC1884.JPG" alt="Bottom plate" >}}
    {{< img src="/images/cocot46plus/_DSC1887.JPG" alt="OLED cover" >}}
    {{< img src="/images/cocot46plus/_DSC1894.JPG" alt="Various parts" >}}
    {{< img src="/images/cocot46plus/_DSC1897.JPG" alt="Trackball holder, mcu, sockets and knobs" >}}
    {{< img src="/images/cocot46plus/_DSC1886.JPG" alt="Bottom cover" >}}
    {{< img src="/images/cocot46plus/_DSC2017.JPG" alt="Lens holder" >}}
{{< /gallery >}}

The keyboard kit contained the following:

- PCB
- Acrylic bottom plate
- FR4 bottom MCU cover
- FR4 switch plate
- FR4 OLED cover plate
- Different sizes screws and standoffs
- Kailh MX hotswap sockets
- Mouse sensor (ADNS-5050) and lens piece (I actually received these twice, not sure if that is intended..)
- Trackball holder (bottom and top)
- Red LED for the mouse sensor
- OLED display
- Reset button
- Rotary encoder
- 2 SK6812MINI-E RGB LEDs
- Anti slip pads

Besides the kits content I prepared:

- 34mm trackballs (4-pack)
- 3D printed rotary encoder knobs (also [from aki27](https://aki27.booth.pm/items/3973033))
- Mill Max Low Profile Sockets and pins
- Sparkfun Pro Micro RP2040
- Kailh Box Whites
- MT3 Susuwatari keycaps
- [Lens holder](https://www.thingiverse.com/thing:5458545)

## Build notes

I mainly followed the official [English build guide](https://github.com/aki27kbd/cocot46plus/blob/main/doc/buildguide_en.md) and I'll take notes here on some deviated paths I took.

### Presoldered parts

The diodes and underglow RGB LEDs come presoldered, this saves some solder time. I believe the Kailh hot swap sockets can also be pre-soldered by [JLCPCB](https://jlcpcb.com/) for example, which would have saved even more time, but I am not sure how much that would increase the price. 
Besides the sockets there isn't much to solder anyway, so it's no big deal.

### RGB Indicator LEDs

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1905.JPG" alt="RGB LEDs" >}}
{{< /gallery >}}

The board has 2 RGB LEDs pointed up, those are used as layer indicators and thus will change color when changing layer.

### Trackball sensor

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1915.JPG" alt="ADNS-5050" >}}
  {{< img src="/images/cocot46plus/_DSC1918.JPG" alt="Lenses" >}}
{{< /gallery >}}

Next I soldered the trackball sensor. I actually received two sensors and two different lenses, but I am not sure why. The second lens was also of a different shape and didn't fit anyway. Perhaps a kitting mistake?

### Mill Max hot swap sockets and RP2040

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1920.JPG" alt="Mill Max sockets" >}}
  {{< img src="/images/cocot46plus/_DSC1923.JPG" alt="Mill Max sockets soldered" >}}
  {{< img src="/images/cocot46plus/_DSC1931.JPG" alt="Mill Max sockets pins" >}}
  {{< img src="/images/cocot46plus/_DSC1926.JPG" alt="Sparkfun Pro Micro RP2040" >}}
  {{< img src="/images/cocot46plus/_DSC1935.JPG" alt="Sparkfun Pro Micro RP2040 placed" >}}
  {{< img src="/images/cocot46plus/_DSC1937.JPG" alt="Sparkfun Pro Micro RP2040 soldered" >}}
{{< /gallery >}}

In the official build guide they use [spring loaded header pins](https://yushakobo.zendesk.com/hc/ja/articles/360044233974-%E3%82%B3%E3%83%B3%E3%82%B9%E3%83%AB%E3%83%BC-%E3%82%B9%E3%83%97%E3%83%AA%E3%83%B3%E3%82%B0%E3%83%94%E3%83%B3%E3%83%98%E3%83%83%E3%83%80-%E3%81%AE%E5%8F%96%E3%82%8A%E4%BB%98%E3%81%91%E6%96%B9%E3%82%92%E6%95%99%E3%81%88%E3%81%A6%E4%B8%8B%E3%81%95%E3%81%84), which seems to be the more popular choice in the Japanese keyboard world. However, these are near impossible to get in Europe. I have used them in the past when I bought them from [Keycapsss](https://keycapsss.com/keyboard-parts/parts/91/spring-loaded-pin-headers-12-pin-2pcs-conthrough?c=11), but they are out of stock since a while with no indication when they will get back in stock. Besides the availability, the PCB has to support them, and there doesn't really seem to be a consensus on the mcu pin hole size here.

Because of that I opted for choosing an alternative, which seems to be the standard in the West, [Mill Max sockets](https://splitkb.com/collections/keyboard-parts/products/mill-max-low-profile-sockets).

The keyboard is built for an Atmega32u4 microcontroller. Since those are getting harder to get and more expensive, due to the chip shortage. Plus I keep running into storage issues with those, I wanted to upgrade to a RP2040 microcontroller. I have some Sparkfuns and [Splinkies](https://github.com/plut0nium/0xB2), but since this board does not use the bottom row of pins which are present on the Splinky, I opted for the Sparkfun.

### LEDs

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1942.JPG" alt="Sensor LED" >}}
  {{< img src="/images/cocot46plus/_DSC1945.JPG" alt="Working LEDs" >}}
  {{< img src="/images/cocot46plus/_DSC1946.JPG" alt="Working LEDs" >}}
{{< /gallery >}}

Soldered the LED for the sensor and checked if all LEDs are functional by plugging in the USB C cable.

### OLED socket and reset button

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1961.jpg" alt="OLED reset" >}}
{{< /gallery >}}

Next step is to solder the socket for the OLED display and the reset button.

### Kailh hot swap sockets

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1951.JPG" alt="Hot swap sockets" >}}
{{< /gallery >}}

Solder all the hot swap sockets. Since the bottom center will house a rotary encoder, no need to solder a hot swap socket there.

### Rotary encoder

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1965.JPG" alt="Rotary encoder" >}}
{{< /gallery >}}

Fit in the rotary encoder and solder it.

### Lens holder

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC2017.JPG" alt="Lens holder" >}}
  {{< img src="/images/cocot46plus/_DSC2019.JPG" alt="Lens holder fitted" >}}
  {{< img src="/images/cocot46plus/_DSC2020.JPG" alt="Lens holder oled" >}}
  {{< img src="/images/cocot46plus/_DSC2027.JPG" alt="Lens holder oled" >}}
{{< /gallery >}}

According to the build guide the lens should be secured with masking tape, but a simple [lens holder](https://aki27.booth.pm/items/3973033) can also be ordered, which holds the lens in place. On [Twitter](https://twitter.com/kepeoo) I found another [lens holder](https://www.thingiverse.com/thing:5458545) which is extended so it can also keep the OLED display straight. 

### Case assembly

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC2005.JPG" alt="Switches placed" >}}
{{< /gallery >}}

As you might have noticed I didn't take any pictures of the case assembly since the official build guide covers it pretty well. The only thing I would change is to place the 6mm spacers around the trackball area on the PCB before attaching the switch plate and the switches. Since there is very little space to place them afterwards.

### Trackball

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC2000.JPG" alt="Trackball" >}}
  {{< img src="/images/cocot46plus/_DSC1897.JPG" alt="Trackball holder, mcu, sockets and knobs" >}}
{{< /gallery >}}

I got a 4-pack of trackballs before I got this keyboard, for the Charybdis, but didn't use them yet. Since I am using the Susuwatari keycaps, which are grey, I also opted for the grey trackball.

The trackball holder has 3 bearings inside (the white dot), so the trackball can move smoothly.

### Converting to RP2040

As I said I wanted to upgrade to an RP2040.

Usually adding 
```c
CONVERT_TO=promicro_rp2040
``` 
to `rules.mk` file is enough to convert an existing keyboard. However when I did this the OLED display showed as following:
{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC1976.JPG" alt="OLED issue" >}}
{{< /gallery >}}

And the trackball would react very choppy and all keys where acting strange, they would be either very delayed or not activate at all. I swapped in an Elite-C to check if it would have the same issues, but it did not.

When enabling debugging on the RP2040 I found the following error coming from the OLED:
```c
> oled_render offset command failed
```
Which seemed to get spammed and caused the issues.

After consulting with the guys on the QMK Discord it appeared a matrix row pin (`D1`) is being shared with I2C. 

On AVR the I2C controller hijacks the pin whenever it is being activated.

On RP2040 however you are supposed to set the appropriate alternate function for the used pins, and that selection gets overwritten when the matrix code reconfigures the pins as plain GPIOs. 

As stated by `sigprof` on Discord.

I added the changes and my Cocot46plus is now running on RP2040!

Many thanks to `bomtarnes`, `Drashna`, `sigprof` and `Dasky` from QMK Discord for helping me out with this issue!

The working firmware with the changes can be found [here.](https://github.com/ykz89/qmk_firmware/commit/5f631849eb30067237aa9d2be39aa08802cb4b2a)

## Conclusion

{{< gallery class="content-gallery" >}}
  {{< img src="/images/cocot46plus/_DSC2015.JPG" alt="cocot46plus" >}}
{{< /gallery >}}

Because of the presoldered parts this build was very easy to do. Using spring loaded headers for the MCU would probably make it even easier, but they're hard to source in Europe. I was glad I socketed the microcontroller however, that way I could easily swap mcus to check if the issues I had were caused by the mcu.

For the RP2040 I did not expect to run into this problem, but luckily it was easily fixed with help. For a future revision it might be nice to upgrade the MCU and use one with more pins so the pins don't have to be shared.

Besides that I very much like the trackball holder and how it traps the trackball so it doesn't fall out when holding it upside down. This makes it easier to carry the board around.

## Next steps
In my [tweet](https://twitter.com/yingkun/status/1562171042348638212) I said my next steps would be to migrate my keymap and upgrade to RP2040. Upgrading can be checked off, so what's left is migrating my keymap.

Besides that I am still thinking of using Gazzew Boba U4s instead of the Kailh Box Whites, but I'll decide on that after I migrated my keymap and typed on it for a while.

Other than that I'll probably add some [middle plates](https://github.com/aki27kbd/cocot46plus/blob/main/doc/cocot46plus_middle.zip?raw=true) and add those.

For those a new post will follow.
