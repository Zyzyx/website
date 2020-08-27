
---
title: "MetaRPG 0.3.0"
date: "2011-04-16T12:06:00-04:00"
draft: false
---

I've been putting off the Windows port for quite a while, and the reason is because I've been watching two technologies grow before pursuing one.

The first is PyGObject, which is a feature of GNOME 3. If I go this route, MetaRPG should be Python and PyGTK-agnostic, meaning you can install any modern versions of these dependencies and it should work just fine. The MetaRPG user experience would not change much; it would make bundling Python and PyGTK with MetaRPG easier though, and it makes development easier in the future. This is the simpler path to take as a developer.

The second is to port over to Moksha on top of TurboGears2. This is much harder work, but in a direction I'd really like to see MetaRPG take. It would basically make MetaRPG a webapp, one that you access in your browser. There are other competing technologies in this space too, I just have not found one I'm certain can do everything I need yet.
