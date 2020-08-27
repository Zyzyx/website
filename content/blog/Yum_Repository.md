
---
title: "Yum Repository"
date: "2011-10-02T12:46:00-04:00"
draft: false
---

For my non-work side projects I find myself packaging software for Fedora from time to time. I created a yum repository for those packages [over here](http://download.brolem.net/Zyzyx/rpms/zyzyx.repo). So far it doesn't contain anything I want to brag about, just dependencies for projects I'm getting involved with. I'll post more about those when I reach some kind of appreciable goal. MetaRPG might end up in there some day too.

For the Fedora-novice, take that text file and save it in <strong>/etc/yum.repos.d</strong>. Once saved you can use <strong>repoquery</strong> (from the <strong>yum-utils</strong> package) to find out what it is providing.

<pre>
$ repoquery --repoid zyzyx -a
</pre>

If you want more info on a package, ask yum:

<pre>
$ yum info evnet
</pre>
