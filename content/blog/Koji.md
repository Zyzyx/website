
---
title: "Koji"
date: "2011-05-04T12:14:00-04:00"
draft: false
---

One of my job functions at work is to maintain and extend our build system. This affords us a couple benefits: one central location to find package and product builds (which is good when multiple teams need to work together for integration tasks), and a repeatable workflow that product groups are familiar with across the company.

Internally, we developed a system that served well for a couple years. After a lot of debate with a few executives, we eventually open sourced this system, calling it Koji. It took a while to do this because folks internally were concerned the company was giving away the "secret sauce" behind building a distribution. Fedora uses Koji today, and you can access the Web UI.

I wrote a couple extensions to it that allow Koji to build images: ISOs, raw disk images, qcow and vmx. Recently Fedora began making use of these extensions for F15. You can see LiveCD and EC2 image tasks in the history.
