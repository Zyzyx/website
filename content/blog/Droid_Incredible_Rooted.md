
---
title: "Droid Incredible Rooted"
date: "2011-01-18T11:54:00-04:00"
draft: false
---

While the Droid Incredible does a lot of cool things and lots of nifty apps exist for it, the one thing it can't do out of the box is remove pre-installed crap courtesy of the carrier. This included integration with Facebook, Twitter, Flickr, and Verizon's own implementations for map navigation and video/picture sharing suites. After 2 days of use, I couldn't take having the bloat anymore.

I followed this guide. For the most part it worked as described, however there are a few addendums I will point out here.

* Download Section: Step 5 and step 6 can be omitted.
* Getting Ready: Step 4 can be omitted.
* unrevoked recovery reflash tool: The application is called reflash_package.exe

The Unrevoked3 folks have not disclosed the nature of the exploit yet but it is clear that it lives the USB drivers used to interface with a computer when it is connected to one. The payload overwrites the recovery image with their own custom one, today that is ClockworkMod. This is why there is a risk of bricking your phone: if the update fails, you don't have a recovery image. If you don't have that and you trash the main interface, you're boned for good. Fork over another $400.

Once ClockworkMod is installed you can get to it by HBOOTing the phone (this is in the guide but not where you'd expect to read it) by holding volume-down and power at the same time. This will take you to a boot menu where you can select Recovery. Use volume-up and volume-down to access it, and the power button to select it. Executing the Recovery option will start up ClockworkMod where the interface is a little different: power is the "back" button, pushing in the joystick (center bottom of the phone) is how you select options.

There are a lot of customization options available to you: custom ROMs, kernels, and Android OS updates. Personally I don't plan to explore many of them, I just wanted Facebook, Flickr, VCast, AmazonMP3 and Twitter out of my face.

