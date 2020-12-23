---
layout: default
title: Sofle RGB Keyboard - build guide
---

Almost all of this build is identical to the original Sofle, I've reduced the sockets to kailh cherry only, and added up to 36 rgb leds.  


## Bill of materials

The following is needed to build the keyboard.


- **2 PCBs**
- **2 top plates**, **2 bottom plates** for a sandvich-case build.

- **2 Pro Micro**board or clone. With 2x12 pins and ATmega32U4 microcontroller. Just make sure you **don't** buy something like Arduino Micro (a different pinout) or Arduino Mini (different microcontroller). You could also use Elite-C which basically Pro Micro with USB-C.
- **4x12 pin header (and optionally socket)** for Pro Micros. There are several ways how to mount Pro Micros to the board. Either the male PIN headers you most likely got with the board from the supplier could be used to solder it directly to the board. Build guides for Helix, Corne and Lily58 suggest [those spring pin headers][springpinheader] which are very compact and give you non-permanent connection (you can remove or replace Pro Micros). Another possible approach [is described at splitkb.com][promicrosocketing].

- **58 keyboard switch sockets by Kailh**. The PCB supports sockets for traditional MX switches. They are available on Aliexpress, KBDFans and others.
- **58 keyboard switches** of your preference, MX. Just make sure you have matching sockets for them.
- **58 keycaps**. You can use either all in `1u` size but it looks nicer with two `1.5u` for the thumb keys.
- **58 diodes  1N4148W**. They are surface mount diodes in SOD123 package.
- **2 TRRS connectors**. The same type which is used for Corne, Lily58 etc. Technically even TRS should work[^1] if you stick to (default) serial communication. 
- **2 tactile buttons** through-hole, 2 pins. Technically optional: you can use metal tweezers whenever you need to reset the microcontroller. There's also a reset key on default layout so as long as you have firmware flashed and working you shouldn't need reset button on the board. 
- **1 TRRS cable**. TRS should work[^1] if you stick with Serial. 
- **10 (+4) M2 spacers**. 10 are going to hold the bottom and the top together. Their height depends on which switches you use. A build guide Lily58 Pro suggests  `7mm` for MX. I was not able to get `7mm`, but `6mm` worked well for me with MX switches. I used brass ones but you can also buy nicer from anodised aluminium. 
- **20 (+8) M2 screws**. 20 are going to hold the boards together (via spacers). I used some I had in my stock so I am not going to tell you exact length. But they need to be long enough to fix a `1.6mm` thick PCB to the spacer and short enough so two of them can fit in one spacer (might be trickier with 4mm spacers for Choc switches)
- **8 - 10 adhesive rubber feet**. They are really important, trust me.
- **Micro USB Cable** to connect the keyboard to a computer.


**Optional**
- **OLED/s**
	- **2 ssd1306 128x32 OLED display module**. Very common everywhere. 
	- **2x4 pin header (and optionally socket)** for OLEDs. I have used the most common 1x4 female pin sockets which are quite tall but they also fit the height of ProMicro with the sockets I have used. Unfortunately, the pin headers on my OLED modules (again those very common square male headers you would get with the modules) are loose in the sockets. It works but it's fiddly. I'll have to find a better solution.
-**Rotary encoders**
	- **2 Rotary encoders EC11**, If you are not sure take EC11E. Some other variants (EC11K) may have some additional plastic pins for and require mounting holes for them (which are not included on the PCB).
	- **A matching knob** for each encoder. 
-**LEDs**
	-**SK2812 mini rgb leds** make sure that you get the style with irregular shaped pads that are flush to the led, and make very sure that you know what the pinout for your varient is. There are at least  2 common pinouts, thankfully just rotated 180 degrees, but for you the pin 1 marking may be on pin 3.
		-**1x forward facing layer indicator**
		-**6x rear facing drop lights**
		-**29x per key lights** 



## Tools and materials

- soldering iron
- solder 
- good tweezers
- masking tape
- isopropyl-alcohol for cleaning
- screwdriver

## Steps

### Prepare

Make sure you know which side you are working on, and don't make two left hand sides by mistake 

### the LEDs** 
Work out what leds you wish to have, I have endeavoured to provide plenty of flexibility, and all led configurations are available using the headers available. If you wish to experiment, use 2.54mm headers and jumpers. If you know what you want, use a solder bridge to enable the leds required.  
The traditional LED header is available, and can be used alone, or theoretically fed back in to one of the other headers if so desired. 

Make sure you know which way around your leds are, different brands have different pin 1 positions. Thankfully it appears that the pad pattern underneath is consistent, so use it. I recommend doing one LED and testing it before continuing. This unfortunately suggests soldering the micro on first, despite it making the back side harder to solder. A good alternative would be to use an existing keyboard with leds to inject the signal and power through the LED header.


The surface mount LEDs are easier to solder, and there are only 1+6 of them on each side, so are a good place to start if you aren't used to soldering them. Use a fairly low temperature (240c) and lots of flux. Place the led in position, heat one of the pads on the board for several seconds before moving the iron to touch the pin on the led , then add solder. Moving the iron back and forth from the pin can help to flow the solder under the LED, 

I have added a single LED to the top surface to act as a layer indicator, this is enabled by bridging 2-3 on J6(indicator bypass).

To enable drop lighting, short pins 1-2 of J4(Light select), to enable only per key lighting short pins 2-3 of J4. 
If you wish to use per key lighting, you also need to short pins 1-2 of 5. 

| indicator | drop lighting | per key 	| j6 	| j4 	|j5 	| 
| ---		| ---			| ---		| --- 	| ---  	| --- 	| 
| Y			|  N			|   N		| 1-2	|	?	| ?		| 
|	Y		|  Y			|	N		|	1-2	|	1-2 | ?		|
|	Y		|	Y			|	Y		|	1-2 |  1-2	| 1-2	|
|	Y		|	N			|	Y 		| 	1-2 |	2-3 | 1-2	|
|	N		|   N			|   Y 		|  2-3	|   2-3 | 1-2   | 
|   N		|   Y			| 	N 		|  2-3	|   1-2 | ?		|
|	N 		|	Y 			|   Y 		|  2-3	| 	1-2	| 1-2 	| 	


the per key lighting is painful and slow for these it is definitely best to do them in order, and test regularly. Use as low a temperature as you can manage, place the board flat on a table, and drop an led in. Create a solder bridge from the led to the board, not spending too much time with the iron on the led (few seconds) otherwise it will burn out. 

if the string stops working, resolder the last working one, and the first to fail, then if needed replace them. 


### Components on the backside

Starting with the diodes. They belong to the backside of the PCB. Make sure you have orientation right - they are all oriented to the same side. The end with the thin line is Cathode (-) and it should go in the direction of the "arrow" symbol on the PCB.

Sockets for switches belong again on the back side, the same side as diodes. Make sure they are flush with PCB and match the orientation shown on the silkscreen. 

### Bridge the oled pads
This is done on the top side, all 4 solder bridges must be completed. This is easier before the pro micro headers are soldered 




### Components on the front side

Button and TRRS sockets belong to the top. Use a piece of tape to fix them and apply solder from the bottom side.


### Pro Micro and displays

The pro micro must be installed with the components facing the pcb, and the plain back side facing out. Theoretically I think these could be installed on the under side for a lower profile. 

make sure that you use the outlined headers from whichever side of the board that you mount the micro on. 



### Rotary encoders

Add rotary encoders last, they are big, and make soldering harder 


### Keyboard switches and plates

![Step 14](images/build_guide/IMG_20191109_154009.jpg )

Snap first switches into corners.

![Step 15](images/build_guide/IMG_20191109_160157.jpg )

Mount the stand-offs to the top plate.

![Step 16](images/build_guide/IMG_20191109_160519.jpg )

Carefully snap the first switches to the sockets. Be careful so you don't bend their contacts. Add more.

![Step 17](images/build_guide/IMG_20191109_160802.jpg )

Until they are all in place.

![Step 18](images/build_guide/IMG_20191109_160811.jpg )

Double-check the bottom. You should see all the contacts in sockets.

![Step 19](images/build_guide/IMG_20191109_161014.jpg )

And mount the bottom plate.

![Step 20](images/build_guide/IMG_20191109_161224.jpg )

Completed half of the keyboard waiting for keycaps.

### Finishing touches

![Step 21](images/build_guide/IMG_20191109_163910.jpg )

Put at least 4 adhesive rubber feet in the corners so the keyboard is not moving when you type.

## Warnings and disclaimers

- Don't connect or disconnect the TRRS cable when the keyboard is powered. It may short out. Always disconnect the USB cable first.
- Be gentle with micro USB ports on your microcontrollers. They are easy to break.
- Keep in mind that this is a prototype of a DIY keyboard. It's not a polished product.

## Firmware and programming

Sofle keyboard uses [QMK Firmware][qmk_firmware] and support for the board is part of the main QMK repository. There's also a basic support in [QMK Configurator][qmk_configurator] but there's no default layout yet and encoders are not supported.

Suggested approach is to build the firmware yourself. You should be familiar with QMK and be able to make it work on your local environment. If not, please [follow the instructions in the documentation][qmkintro].

- Make sure your QMK environment [is setup][qmkintro].
- Make sure halves are not connected together with TRRS cable.
- Connect one half to USB, flash the firmware: `make sofle:defaultRGB:avrdude` (you may need to use `sudo` depending on your setup). Use the reset button to reset the keyboard when you are asked to in console.
- Connect the second half and flash it in the same way as the previous one.
- Disconnect the USB cable. Connect both halves together with TRRS cable.
- Connect USB cable to the **left** side[^2]. 
- Enjoy SofleKeyboard!

## Troubleshooting

### Elite-C v3.0

Elite-C v3.0 had problems when used with split bords (on both halves). Those are fixed in version 3.1. For v3.0 add `#define SPLIT_USB_DETECT` to `config.h` file. I don't have Elite-C so this is untested, but should work.

### Typing lag when used without OLED 

If you chose to not use OLED for both halves you should disable support for oled (set `OLED_DRIVER_ENABLE` to `no` in `keymaps/defualt/rules.mk`).

If you don't use OLED only on one half you are need to do **one** of the following to fix the lag:

- Solder pull-up resistors (4k7) to the PCB (R1, R2) without OLED.
- Use a workaround explained [in this issue][nooledlag].
- Stop using OLED completely and turn it off as described above.

## Links

- [Github with KiCad projects][soflegithub]
- [Layout in KeyboardLayout editor][soflelayout]
- [QMK Firmware][qmk_firmware]
- [QMK Configurator][qmk_configurator]

## Footnotes

[^1]: Serial is the default behaviour. If serial is used, you don't need TRRS cable (4 contacts, used for headphones with a microphone) but just TRS (stereo audio jack). 
[^2]: This can be changed, look for [setting handednesss][qmkhandedness] in QMK documentation.
[^3]: There was a design issue where the cutout for the encoder is big enough only for the base of the encoder but not for its legs. That is perfectly ok when you build the board with MX switches since the plate sits above the legs. But for low profile Kailh Choc switches there's no longer any gap between plates. If you have unfixed plate (the problem was fixed in v1.1.) and wish to use an encoder, you'll need to file off a bit of PCB material to get the legs of encdor through (see the guide above).

[layoutarticle]: <https://josef-adamcik.cz/electronics/in-search-of-the-best-custom-keyboard-layout.html> "In search of the best custom keyboard layout"
[introductionarticle]: <https://josef-adamcik.cz/electronics/let-me-introduce-you-sofle-keyboard-split-keyboard-based-on-lily58.html> "Let me introduce you SofleKeyboard - a split keyboard based on Lily58 and Crkbd"
[soflelayout]: http://www.keyboard-layout-editor.com/#/gists/76efb423a46cbbea75465cb468eef7ff "Sofle Keyboard layout at keyboard-layout-editor.com"
[soflegerber]: https://github.com/josefadamcik/SofleKeyboard/releases "SofleKeyboard - gerber files"
[qmk_firmware]: https://github.com/qmk/qmk_firmware/ "QMK firmware"
{:target="_blank"}
[qmk_configurator]: https://config.qmk.fm/#/sofle/rev1/LAYOUT "QMK configurator"
{:target="_blank"}
[springpinheader]: <https://yushakobo.jp/shop/a01mc-00/> "Spring pin headers - Japaneese"
{:target="_blank"}
[qmkprotonc]: https://qmk.fm/proton-c/ "QMK Proton-C"
{:target="_blank"}
[promicrosocketing]: <https://docs.splitkb.com/hc/en-us/articles/360011263059> "How do I socket a microcontroller? by splitkb.com"
{:target="_blank"}
[qmkintro]: <https://beta.docs.qmk.fm/newbs/newbs_getting_started> "QMK getting started"
{:target="_blank"}
[qmkhandedness]: <https://docs.qmk.fm/#/feature_split_keyboard?id=setting-handedness> "QMK firmware - setting handedness"
{:target="_blank"}
[manufacturingproblems]: https://josef-adamcik.cz/electronics/corne-keyboard-build-log.html#manufacturing-at-jlcpcb---update-27112019 "Possible problems when manufacturing top plate for Corne"
[nooledlag]: https://github.com/qmk/qmk_firmware/issues/7522 "No OLED lag bug"
[soflegithub]: https://github.com/josefadamcik/SofleKeyboard "SofleKeyboard - KiCad project on Github.com"
[sourcing]: <{{ site.baseurl }}/sourcing_parts.html> "Sourcing parts"
