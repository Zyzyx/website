
---
title: "Eureka"
date: "2013-12-30T14:08:00-04:00"
draft: false
---

A few months ago a friend and I started talking about Doom, the classic game from the early 90s. Later that week I was over his house, where he was playing the game on his laptop. I go through this phase as well, every 2 years or so revisiting the game and playing a bunch of patch wads (custom maps) from the [idgames archives](http://www.doomworld.com/idgames/index.php?dir=levels/doom2/).

In the later stages of the phase I grab a doom map editor and work on one. Imagine my surprise when I saw a <a href="http://eureka-editor.sourceforge.net/">new release of an editor for linux</a>, as recent as August, 2013. Behold, Eureka!

Naturally, I had to package that up and put it in Fedora, and I finally got around to following up on that during my christmas break. <a href="https://bugzilla.redhat.com/show_bug.cgi?id=1004565">Eureka was accepted in the distro a few weeks ago</a>, and I'm now working on building it in Koji.

If you dig around the Eureka homepage, there are two other doom editing tools available: Visplane Explorer and Oblige, which generates random maps of doom on the fly based on some user input. In time I may package those up too. I have a silly plan to create Doom In the Cloud, a web frontend where you check a few boxes and get a few wads (levels) in return, generated in the cloud. THE CLOUD.
