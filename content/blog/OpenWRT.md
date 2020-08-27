
---
title: "OpenWRT"
date: "2014-10-14T14:22:00-04:00"
draft: false
---

Yes, I'm writing this during a marathon of meetings at the office. I'm advocating an Open Source project, so that is close enough to work for now. There's more benefit to the company than these meetings at least.

Last weekend I flashed my router, an [ASUS NT-16](http://www.asus.com/us/Networking/RTN16/), with <a href="https://openwrt.org/">OpenWRT</a>. It was <a href="http://blogs-brolem.rhcloud.com/node/831">previously flashed with TomatoUSB</a>, but I found out a few months ago that development had pretty much ended. I'm not sure where interest went, but I saw that OpenWRT gets a lot of sponsorship from the <a href="https://www.eff.org/">EFF</a>, so I figured it was a good bet. I really wanted to get off of Tomato after the rash of security flaws with trendy names, and OpenWRT was just finishing up their latest release.

OpenWRT also has a release naming scheme that I am a big fan of. Like Ubuntu, they go with alphabetical alliterations, but instead of adjective-animal, they use cocktail names. The current release is Barrier Breaker, so once I finished flashing, I had a cocktail suggestion to celebrate the occasion, which I did on Saturday at 10:30am.

Flashing was pretty easy this time around, only 3 easy steps: download the image, write it to the "linux" MTD, and then reboot. I had to do a little <a href="http://wiki.openwrt.org/toh/asus/rt-n16">data mining</a> to figure out what <a href="http://wireless.kernel.org/en/users/Drivers/b43/soc">subarchitecture</a> my router was. The MTD command was:
<ul><li>mtd-write -i openwrt-brcm47xx-mips74k-squashfs.trx -d linux</li></ul>

The <a href="http://wiki.openwrt.org/doc/howto/basic.config">installation and configuration documentation for OpenWRT</a> is very good. I was impressed with the breadth of information. I still have a step to go, the image I used comes with the open source b43 broadcom driver, which does not support wireless-N nor multiple SSIDs. Since I'd like to have both of those things, I need to use either the brcmsmac module, or Broadcom's closed-source drivers. I expect to hack that together this coming weekend. So far the router has been working fine, a few devices around the house needed a reset to figure out that the wireless encryption algorithm had changed, but otherwise the transition has been pretty smooth.
