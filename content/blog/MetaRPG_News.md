
---
title: "MetaRPG News"
date: "2010-04-30T11:23:00-04:00"
draft: false
---

MetaRPG is coming along well. In the last few weeks I've spent weekends working on the server code, and I've taken an approach that so far, is functioning. There is still a lot to do, but I'm happy to report that the client side is feature complete for the first release. This means I don't intend to add any new functionality to it, only supporting code to work with the server and bugfixes. In other words if you intend to play only with yourself, the program does its job well enough. For those interested, I went with a threaded SocketServer implementation.

There are quite a bit of tasks left before we'll use it to play though, to name a few:

* Send and receive stats from other players
* plenty of bug fixes
* port to Windows

I decided to host the project on FedoraHosted site. With this I have all I need to run an open source project: wiki documentation, trac for bug/feature tracking, and a gitweb front end to the sources in git. Also, since Fedora is used to being legally attacked, I figured they'd be the right people to host my project with. Note that anyone can start an OSS project here, you don't have to work at Red Hat.

I'm going to work toward releasing the first Fedora version by the end of the summer. Hopefully a community will assist with improving it further, maybe even port it to Windows for me. It's gratifying to see it really coming together finally.
