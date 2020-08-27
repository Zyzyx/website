
---
title: "Hardware Hell"
date: "2010-10-31T11:46:00-04:00"
draft: false
---

My dubiously functioning hardware gave me a scare this afternoon as I tried to install 4 more gigabytes of RAM.

Presently it only has 2G, so I figured it was time for an upgrade to 6G before installing Win 7. Once I installed the pair of 2G sticks however, all was not well. Powering the computer on would lead to one of two results, I could not discern a pattern: never display anything or beep, or print out the the following to the console:
```
Award BootBlock BIOS v1.0
BIOS ROM Checksum error
Detecting Floppy drive A media ... failed
Detecting CDROM media ... failed

System halting
```
It occurred to me that this may be expected to happen since the hardware profile has changed, but there was no way for me to get into the BIOS set up utility. Please trust me when I say I know how to get into my system's BIOS. :) It really wasn't possible.

So I decided to reset the CMOS. For my motherboard which is an ASUS P5N-E the steps are:

1. Disconnect power, remove CMOS battery
2. Move CMOS reset jumper (located under SATA ports) from 1-2 position to 2-3
3. Wait 20 seconds
4. Move CMOS reset jumper back to position 1-2
5. Replace CMOS battery, reconnect power

I completed these steps and booted successfully into the BIOS set up. I was starting to feel relieved when the BIOS setup utility actually hung after 17 seconds. I rebooted several times and experienced the same thing (or the useless black screen again). I attempted to replace the CMOS battery itself (and reset CMOS again) but this did not change the behavior.

Now I'm starting to worry because I do not like the risk associated with flashing my BIOS, which appeared to be my next option. Instead I removed the RAM, reset and rebooted. After restoring my old BIOS settings, I was able to boot back up normally with just my old RAM. Relief!

So here I am with the 2G sticks in front of me, and I'm wondering if I should try again. Pensively I was looking at the packaging, and I noticed the corner of it looks like it suffered an impact. The electronics look ok though. I'm strongly inclined to RMA the RAM and try again with replacements.

Have you guys heard of new RAM trashing your BIOS like that, or have another explanation for what I experienced? The setup utility hanging is rather scary, but I don't understand how bad RAM could do that. The intermittent black-screen boots make me think there is a power issue. My PSU is 550W. The other hardware is:

* GeForce 8800 GTX
* 1 SATA, 1 IDE hard drive
* DVD ROM, external HD, few USB peripherals
* Intel QX6700 CPU

