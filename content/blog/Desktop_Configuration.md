
---
title: "Desktop Configuration"
date: "2011-06-12T12:27:00-04:00"
draft: false
---

I just installed Fedora 15 with Gnome Shell. While it does function and I can do the basics of what I like, there is still quite a bit to go with respect to configuration, preferences, and optimization. This post is meant to be a reminder for me when I reinstall next year, and a reference for anyone else doing an installation themselves.
Sound and video

**Enable RPMFusion**
```
 # yum localinstall --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm
```
**Install audacious, vlc, and non-free plugins**
```
 # yum install vlc audacious audacious-plugins-freeworld-mp3
```
**Enable NVidia drivers (Warning)**
Add the following to the kernel call in grub.conf
```
rdblacklist=nouveau vga=0×318
```
***Install drivers***
```
# yum install kmod-nvidia xorg-x11-drv-nvidia-libs.i686 xorg-x11-drv-nvidia-libs.x86_64
# reboot
```
***DVD Ripping***
Install DVD::Rip
```
# yum install dvdrip
```
Start it and check the Debug->Check dependencies option. Install anything you are missing. libdvdcss is required to rip encrypted DVDs, but it is illegal distribute this package in many countries. The Livna repository still does though, you can activate it similar to RPMFusion.
```
# rpm -ivh http://rpm.livna.org/livna-release.rpm
# yum install libdvdcss
```
**Browser Tweaks**

* Set up Firefox Sync (now built into FF4) BlackBrick has the key.
* Install IE Tab 2, Firebug, Stylish, Greasemonkey, and AdBlock Plus
* Set homepage, set start up behavior
* Install flash. Adobe sucks.

```
# yum localinstall --nogpgcheck http://linuxdownload.adobe.com/adobe-release/adobe-release-i386-1.0-1.noarch.rpm
    # rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-adobe-linux
    # yum install flash-plugin nspluginwrapper.x86_64 nspluginwrapper.i686 alsa-plugins-pulseaudio.i686 libcurl.i686
```
**Fedora Development**
Install developmental tools
```
# yum install development-tools
# yum install rpm-build rpmdevtools rpmlint
mock koji
```
Added yourself to mock group
```
# usermod -a -G mock username
```
Set up:
```
$ rpmdev-setuptree
```
**Gnome Tweaks**
Stock themes
Download a theme and put it in /usr/share/themes Include gtk-2.0, metacity, etc directories in it if included. Atolm is a good dark one.
Install the tweak tool to be able to select installed themes
```
# yum install gnome-tweak-tool
```
Theme customization is nearly non-existent, so we have to do this by hand. Example: Tweak window borders and title bar padding. Edit /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml
```
distance name="left_width" value="2"
distance name="right_width" value="2"
distance name="bottom_height" value="3"
distance name="title_vertical_pad" value="6"
```
Configure Nautilus to always show lists, show hidden files and octal permissions
Show "Power Off..." option in status menu by default
Install gnome-shell-extensions-alternative-status-menu
```
# yum install gnome-shell-extensions-alternative-status-menu
```
Copy /usr/share/gnome-shell/extensions/alternative-status-menu gnome-shell-extensions.gnome.org to another directory beside it
Comment out the following line in extenstion.js in the Suspend and Hibernate code sections:
```
this.menu.addMenuItem(item);
```
Set the uuid field in metadata.json to the same thing you called the directory you made in step 2
Remove the RPM; we don't need it anymore.
```
# yum erase gnome-shell-extensions-alternative-status-menu
```
Restart gnome-shell (alt-F2, "restart")

