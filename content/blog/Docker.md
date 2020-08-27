
---
title: "Docker"
date: "2014-01-15T14:12:00-04:00"
draft: false
---

Permit me to talk shop for a while. [Docker](https://www.docker.io/) is a project that makes an interesting use of Linux containers to package up applications and services. <a href="http://en.wikipedia.org/wiki/LXC">Containers in Linux</a> are an artificial way to create a space in which a process can run with limited resources exposed. You can create a container that has network access but only limited bandwidth, or can only occupy one core of your CPU. It's a lightweight form of virtualization, but it's not exactly the same thing. Containers are a relatively new concept for linux, they've been around since the 2.6.24 kernel, but the idea existed well before in other incarnations like BSD jails.

Containers have a lot of potential. You can manage an application by putting limits on the hardware resources that are exposed to it. It's like a virtual machine, except you don't need the whole OS any more. You do not "boot" it. 

What Docker did was automate launching applications in containers, and the thing you feed to docker to launch them is a collection of files. It could be merely a tarball (like a zip), or a complete filesystem. The implications here are very interesting from a distribution standpoint. At Red Hat we could parcel up our software into docker images (that's the term describing the file-pile you give to docker to launch an application) and distribute those instead of a stream of RPMs. 

Say you want a MySQL server. Well, take this docker image that is just the files mysql needs, and launch it. The files on there include the configuration stuff you need, or if not, just edit it and start the service. Would you like 2 mysql servers? Launch another docker image. Extrapolating from that, Red Hat could distribute their layered products as docker images too. Some of these products are not easy to install and configure correctly the first time, but with a docker image, we could distribute a fully functioning instance of the product to you. This could mean a lot to system administrators. If the software is packaged and prepared sensibly, it makes deployment easier than virtualization, and far more efficient because you don't need an entire OS to start it. 

Note however, there is no guarantee they are as secure as isolating services in different VMs. In fact I'm pretty sure they're not, architecturally speaking. However for some use cases the multi-tenancy benefits or the ease of deployment benefits may outweigh that risk. For multi-tenancy I'm talking about having say, 20 web applications on a single system, and using containers to make sure none of them dominate the hardware. You could sort of do this already with rlimits or a heavy weight VM management solution, but my point is containers make it a lot easier.

2014 could be an interesting year for rel-eng at Red Hat. We may be starting a path that will lead to completely changing how we distribute and support our software.
