
---
title: "Where to Have Development Conversations"
date: "2013-05-06T14:01:00-04:00"
draft: false
---

This post is mine with my opinions. They are not Red Hat's. It relates the decision by Anaconda to not hide the root password when you enter it with stars or "bullets".

It's not uncommon to disagree with how a developer decides to add features or changes to their project. When that happens, most people have the decency to engage the developer(s) in a forum they are actively monitoring. They make their case engaging each other like adults, and come to some kind of resolution.

What people shouldn't do is bitch in a [mailing list with a wide audience](http://lists.fedoraproject.org/pipermail/devel/2013-May/182196.html) if you don't get your way. Nor should one <a href="http://it.slashdot.org/story/13/05/04/1248242/fedora-19-to-stop-masking-passwords">escalate it</a> to your pals at slashdot if you're still not satisfied. If someone <a href="http://lists.fedoraproject.org/pipermail/devel/2013-May/182226.html">explains</a> a <a href="http://lists.fedoraproject.org/pipermail/devel/2013-May/182229.html">better way to engage the developers</a>, most users will not respond <a href="http://lists.fedoraproject.org/pipermail/devel/2013-May/182234.html">rudely</a>.

Zero sites I read that carried this story over the weekend mentioned the rationale behind the change: it makes keyboard layout issues very clear. If Anaconda incorrectly sets the keyboard layout, or the user incorrectly set up international character maps, you have no way of knowing until you try to log into the newly installed system, because it won't accept the password. This is a crappy experience. There was a compromise proposed which suggested a "hide" button or something that would let you hide or hide the field so that you could check your work when you felt it was safe. This is a reasonable suggestion, but that appeared nowhere in the initial conversation.

Another thing: the developers decide what goes in and what goes out. Bitching on a mailing and getting the internet mad with you does not make you right. If you <a href="http://lists.fedoraproject.org/pipermail/devel/2013-May/182292.html">try to get the distro to revert the change you don't like</a>, the maintainers are still well within their power to continue ignoring you. In that case, the distro would have to maintain a fork that does not include the changes. This isn't a good thing, and I don't think that's how this will resolve at all; my point is that threatening the maintainers with this course of action doesn't help your cause at all.

I haven't visited slashdot in at least 2 years, but I know several people that would give up their reddit accounts just to be mentioned once. Spoiler: it's not that much fun. You get email and irc pings constantly with people that are either curious, angry, confused, or making snide jokes. Really though, after you've heard one comment you've heard them all; the best way to deal with it is to ignore it completely. I have not had my work slashdotted, nor do I intend to, but I know many that have, and I've never heard them say it was a great experience. I've eaten dinner with Chris every Friday night for 3 years, and he's not out to screw users or flip off security profressionals.

I agree the change was contentious and there is a way to escalate issues appropriately. But you have to have a reasonable engagement in the first place. If they disagree, fine, but don't ignore their arguments when it is convenient and then whine in public places.

For what it's worth, the change was reverted.
