
---
title: "Gource"
date: "2010-01-27T11:11:00-04:00"
draft: false
---

This post has a youtube link below that I need to explain before you click on it. It does not involve cats, yelling, dubbing over star trek, griefing in Second Life, crying teens, shitting on someone's porch, Jackass-quality stunts, violence, anal sex, awful mashups, or Halo headshots. So basically nobody is going to give a shit about it except me.

It was generated using Gource, a program that takes the commit logs of an SCM and generates a visualization of activity over a given people of time. An SCM is a Source Code (or Control depending on who you ask) Manager; a program that tracks changes to a directory tree of source code. I use one while developing MetaRPG; every time I change code around and it works well enough for me to be happy with, I commit those changes to git. That way, at any time, I can revert back to the way the code was that I just saved. It's like having a ton of save games that I can revert to at any point in case I want to do something different while writing code.

Anyway the history of commits is recorded in an SCM, and that info is parsed by Gource to create a visualization. What you'll see is a moving map of, for lack of a better term, nodes. Each node is a file or directory of source code. You'll see icons of contributors zooming around lasering those nodes. That represents a commit to the SCM. Yellow lasers are modifications to the files. Green are when a new file is created, red is when one is deleted.

Below is the Gource visualization for Koji, the buildsystem we use for building packages in Fedora. I have personally contributed to this project as part of my work at Red Hat, so you'll see me included briefly at the end. You'll also see Mike Bonnet, whom I work with very often. He is invited to the wedding.

Koji's Gource.

I hope you enjoy it. Yes I know it needs music. When MetaRPG gets some traction I may create one for it too.

