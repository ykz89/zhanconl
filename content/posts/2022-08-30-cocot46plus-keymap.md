---
title: Cocot46plus Keymap
description: Migrating my Charybdis keymap to Cocot46plus
draft: true
date: 2022-08-30T13:33:38.849Z
tags:
  - keyboard
categories:
  - Keyboard
lastmod: 2022-09-02T22:37:59.996Z
---

# Keymap

I very much like the via keymap of the [Charybdis 3x5](https://github.com/qmk/qmk_firmware/tree/master/keyboards/bastardkb/charybdis/3x5/keymaps/via) created by [Charly](https://github.com/0xcharly). It is inspired on Miryoku which I used before changing to this particular layout, it seems to be more pointing device focussed with the pointer layer instead of the mouse layer. 

So I wanted to migrate that layout to the Cocot46plus.
Since I am not very familiar with the `c` language, I opted for the easiest solution and that is to borrow the code from the Charybdis and apply everything that is missing from the Cocot46plus.

This resulted in the following layout:

{{< img src="/images/cocot46plus/cocot46plus-miryoku-inspired.png" alt="cocot46plus layout" >}}

### Changes from the Charybdis layout

Compared to the layout of Charybdis I applied the following changes:

- Change to Colemak
- Add/Change third thumb key on the right to be delete on tap
- Add keys for the extra columns
- Add a button to rotate the trackball angle (not working yet)
- Add the dedicated mouse buttons
- Add rotary encoder functions
- Give extra thumb keys a function

As you might have noticed the outermost right thumbkey is unassigned, I plan to add a toggle for a gaming layer there.
The one on the left side is a dedicated button to activate [Caps word](https://docs.qmk.fm/#/feature_caps_word?id=caps-word).

And I will probably remove the excess mouse buttons on the pointer layer, since I have dedicated mouse buttons anyway.

### Indicator LEDs

Originally there are only four layers, I now have seven with perhaps more coming up. Every layer has its own color on the image above, I think it was nice to use these colors with the indicating LEDs too, altho the difference between yellow and orange, and pink and purple are pretty hard to see.