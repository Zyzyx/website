
---
title: "FUDCon 2013"
date: "2013-01-22T13:57:00-04:00"
draft: false
---

Last week I was in Lawrence, Kansas attending the Fedora Users and Developers Conference and not enjoying Kansas BBQ because it was too far away from the city. However, the [event itself](http://fedoraproject.org/wiki/FUDCon:Lawrence_2013) was productive.

Like all FUDCons, it was barcamp style talks. I'll recap the ones I attended first:
* Cloud Server Stacks for F19
* Secure Boot Q and A
* Overhauling the Release Model
* Coprs
* Intro to the Installer

Secure Boot and the Installer did not reveal anything novel to me. If you follow <a href="http://mjg59.dreamwidth.org/">Matthew Garrett's blog</a> you already know everything that was covered. Cloud Server Stacks was about OpenStack and Eucalpytus support in Fedora, but it got sidetracked into doing introductions of <a href="http://imgfac.org/">ImageFactory and Oz</a> from the <a href="http://www.aeolusproject.org/">Aeolus project</a> when the conversation steered towards how cloudy images are built.

Coprs was an interesting talk about building 3rd party packages for Fedora. They're like Ubuntu's PPAs, but not quite the same. <a href="http://skvidal.wordpress.com/">Seth Vidal</a> essentially wrote a separate build system to create and maintain them. As a Koji contributor I feel like this came about because of Koji's own shortcomings. We don't want to build 3rd party stuff in Koji because we don't trust it, but really Koji should be secure enough to support this use case. I recognize the cat-and-mouse model of security professionals versus jerks, but I still think this can be done:

# Enable SELinux on the builders and hub. This will require an SELinux policy for mock.
# Using post-build plugins, run ClamAV and Coverity on the build results
# Using tag policy, do not all 3rd party results to be inherited into the base distro

The release overhaul was interesting too, but it also go sidetracked with counter-arguments and hand waving. The idea was to shift from a 20, 21, 22, 23 [...] release cycle every 6 months to a 20.0, 20.1, 20.2, 20.3, 21.0, 21.1 [...] cycle. Each release would still be 6 months apart, but over the 24 month period 20 was active, larger features could be scoped and planned. 20.0 and 20.1 would be rough, disruptive releases, but 20.2 and 20.3 would be the polished releases. This would help users understand what they were in for before installing something like Fedora 15, which would be considered by many to be a disruptive release. (Gnome 3 came out and the number of unique IPs getting yum updates fell by more than 40%. That number is under some dispute.) It remains to be seen if this proposal moves forward.

After the talks were the hackfests, but for me they were more like yakfests. Lots of talking and planning, little coding. This still saved me weeks of email thread exchanges from the office though, so I count it a win. The output is <a href="https://fedoraproject.org/wiki/Features/FirstClassCloudImages">this Fedora 19 feature request</a> which will soon be put to a vote by <a href="https://fedoraproject.org/wiki/Fedora_Engineering_Steering_Committee">FESCO</a>. All of the Koji integration work is to be done by me, with Ian McLeod implementing requested featured on the ImageFactory/Oz side.

Exciting!

A bunch of G+ related posts can be found with the <a href="https://plus.google.com/u/0/s/%23fudcon">#FUDCon</a> hashtag.
