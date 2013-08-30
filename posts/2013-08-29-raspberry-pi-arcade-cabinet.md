# The 4-Player Raspberry Pi Arcade Cabinet

<p class="image">
  ![cabinet](https://dl.dropbox.com/s/33r5xd8x5b6yzj8/cabinet.jpg)
</p>

Back in college, I built a stand-up 4-player arcade cabinet that I egomaniacally dubbed "The Shipstravaganza." It was one of the few major physical projects I've undertaken, and I couldn't have accomplished it without help from a couple of friends. Inside the cabinet sat a Frankenstein PC I built from spare parts: an AMD Athlon 2900+ engineering chip I got from a friend and 512MB of RAM. It was slightly underpowered at the time, but it was *just* powerful enough to play older MAME ROMs, along with NES, SNES, Genesis, and more.

Fast forward to 2013. The machine was on its last legs. It originally ran Windows XP without a front-end &mdash; just ObjectDock and a mouse. I tried installing Lubuntu, but couldn't find a front-end I liked, and ran into some weird issues with [WahCade!](http://www.anti-particle.com/wahcade.shtml) that I was having trouble debugging. I tried to reinstall XP, but the CD-ROM drive was broken, and you can't install XP from a USB stick.

I did a bit of research and stumbled across the [RetroPie](http://blog.petrockblock.com/retropie/) project. Since I've been wanting a Raspberry Pi since first hearing about it last summer, I decided to take the plunge and try it out. I ordered the $35 [Raspberry Pi Model B](https://www.sparkfun.com/products/11546) from Sparkfun, installed [Raspbian via NOOBS](http://www.raspberrypi.org/downloads), and got started.

I decided to use the [RetroPie-Setup](https://github.com/petrockblog/RetroPie-Setup) script just to minimize my investment on the software side, given my previous issues with XP and Lubuntu. The instructions were dead simple &mdash; just make sure you've bumped your memory split per the instructions before you start installing. I decided to compile the emulator binaries from source. Be warned: if you decide to compile ALL THE EMULATORS!, it will take nearly an entire day. I'd recommend pruning down if you don't plan to use some of the more obscure emulators like Apple IIc, PCx86, and Amiga.

Once the compilation was done, I uploaded a few ROMs just to test everything out. I had a bit of slowdown in MAME and the SNES emulator, so I decided to use the Raspberry Pi's software overclocking capabilities to speed things up. I bumped up one level to 800MHz. My performance has been pretty good since then, but YMMV!

The next step for me was to configure the joystick from my arcade cabinet. My original build used an [I-PAC4](http://www.ultimarc.com/ipac1.html) from Ultimarc, which is a keyboard encoder that lets you map arcade buttons to keyboard inputs. Here's a picture:

<p class="image">
  ![I-PAC4](https://dl.dropbox.com/s/08ssvzoagmu3xhe/ipac4.jpg)
</p>

(**Side note**: I had no soldering skills at the time I completed this project, so I hand-rolled, crimped, and daisy chained wires together for 33 buttons and 4 joysticks. My fingers had blisters for days. I wouldn't recommend it to anyone else, but I'm glad I did it!)

My I-PAC4 has an old-school PS/2 connector, so I needed to buy a PS/2-to-USB adapter, which worked out of the box. The main emulation engine in RetroPie is RetroArch + libretro. The default configuration for the iPac4 has a few mysterious button choices that RetroArch doesn't support, so I had to download the [WinIPAC Interactive Panel Designer](http://www.ultimarc.com/download.html) to update my configuration. (The OSX implementation is hopelessly out of date and only runs on PowerPC. I didn't try the Linux utility because I had a Windows machine available and had used the Windows version before.)

I tried editing the retroarch.cfg file in ~/RetroPie/configs/all, but it wasn't working for me, so I edited /etc/retroarch.cfg directly. When programming the I-PAC, I made sure to bind keys that are available to RetroArch. [This file](https://github.com/libretro/RetroArch/blob/e911eda7f41a9e0750ddf01880827b6e8ac1bfc4/input/input_common.c#L616) has all of the available mappings. One other curiosity &mdash; there are key assignments that are commented out in retroarch.cfg, but they are actually in effect. An example:

    # input_menu_toggle = f1

I originally assigned my P1 Start button to F1, and it took me a few minutes to realize that it was being overridden in the retroarch.cfg. Make sure you uncomment these lines and set the values to nul if you plan to use any of those keys in your I-PAC mapping:

    # not a typo!
    input_menu_toggle = nul

At this point, all the games were playable with my joystick. I only had one task left before declaring success: hooking up a physical power button. My Raspberry Pi sits inside a sealed cabinet with no keyboard attached. I did install a Wifi module from [Adafruit](http://www.adafruit.com/products/814) using the instructions [here](http://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/setting-up-wifi-with-occidentalis) and enabled the ssh agent in raspi-config, so I could've ssh'ed into the Raspberry Pi to shut it down each time, but this seemed inconvenient.

In my original build, I cut the wires from my PC's power button to the motherboard and wired them up to the arcade button in my joystick. The Raspberry Pi doesn't have a power button, but it does have some exposed GPIO pins we can use. Luckily, one of the GPIO pins has a pullup resistor built-in, so I didn't even need to breadboard/solder a circuit. I used [these instructions](http://www.raspberrypi.org/phpBB3/viewtopic.php?f=37&t=42449) and a slightly modified version of [this script](https://github.com/g0to/misc_scripts/blob/master/raspi_gpio_actions_INT.py) to set up my power button. I bought a PC power jumper, cut it, rolled the wires together, and used some shrink tubing to make it work. All told, it took about 5-10 minutes of actual effort.

One downside to the GPIO pins is that you can't read them via software when the machine is powered off. (Duh.) Luckily, the setup I went with fits my situation, so I didn't need to worry about it. My arcade cabinet has a power strip inside and a hole in the back. When I want to play a game, I plug in the power strip, which automatically powers on the Raspberry Pi. I play, then press the power button when I'm ready to shut down. Once the Raspberry Pi finishes the shutdown procedure, I unplug the cabinet, and I'm ready for the next time.

If you're thinking about putting a MAME cabinet together, I'd highly recommend considering the Raspberry Pi. It's not powerful enough to run some more modern arcade games and I haven't bothered with added complexities like [CHDs](http://en.wikipedia.org/wiki/MAME#Game_data) (not to be confused with [CHUDs](http://en.wikipedia.org/wiki/C.H.U.D.)). But overall, it was fairly easy to set up and it seems to be a popular target for emulation right now.

Here's the old ~$500 machine I replaced with a tiny little $35 Raspberry Pi:

<p class="image">
  ![Old PC](https://dl.dropbox.com/s/qvbmlqckimwtg85/old_pc.jpg)
</p>

I love technology.

If you have any questions about my setup or the issues I ran into, feel free to contact me on [Twitter](https://twitter.com/kyleashipley). Thanks for reading!