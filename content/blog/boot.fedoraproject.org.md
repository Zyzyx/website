
---
title: "boot.fedoraproject.org"
date: "2013-06-06T14:04:00-04:00"
draft: false
---

A week ago I reinstalled my home desktop with Fedora 18, but this installation marks the first time I did without downloading any of the traditional installation media. No CD, DVD or ISO image. I started the process by downloading a 364k file.

[boot.fedoraproject.org](http://boot.fedoraproject.org/index) (BFO) is a site designed to be booted from using iPXE, based on the work at boot.kernel.org (or BKO). I don't really know what that means either but in short, the little file I downloaded contains just enough of an operating system to get you to a working network stack, which then is used to connect your system to BFO to download additional grub (which is a boot loader) information. If successful, you'll be presented with a grub menu like in many traditional linux boot sequences.

This menu contains references to all Fedora installers since Fedora 13, so you boot any of those. Each of these menu entries is a link to the Anaconda installer which is pre-programmed to download additional content from the usual Fedora mirrors, which you can then use to reinstall a system like usual. Conveniently, you can edit the grub menu entries and add an inst.ks option which will pass in a kickstart file to Anaconda. Kickstarts are used to automate installations-- it is a way to pre-select everything you normally would in the installation wizard. I may post that file in a future update, but right now it has a little too much sensitive information (like account passwords) in it.

I completed this procedure with Fedora 18:
<ol>
  <li>Boot up off of the lkrn file</li>
  <li>Edit the Fedora 18 grub entry to use my kickstart I hosted on this site (and then took down)</li>
  <li>Waited 30 minutes</li>
  <li>Booted into a new F18 installation customized the way I like it</li>
</ol>

Ideally, when Fedora 19 rolls out I'll be able to repeat the procedure with little fuss. The underlying operating system will change, but most of my customizations and tweaks will still be intact. To make this even easier, it really helps to have a home NAS to host your home directory and important things like a music library. To that end, I recommend the <a href="http://www.synology.com/products/product.php?product_name=DS413&lang=us">Synology DS413</a>.

Once other thing: in addition to Fedora installations, BFO also has options to boot in rescue mode for the various Fedora releases. If you set up your grub to have a BFO entry, you can easily get to rescue mode without the corresponding install media if you accidentally hose your system. This detail is implied in the BFO FAQ when it explains how to add the lkrn file to grub. Download bfo.lkrn first and stash it in your /boot directory. Then run:

<code># grubby --add-kernel=/boot/bfo.lkrn --title="Boot BFO"</code>

In grub you should have a BFO option available. You can boot with it and browse around without risk to your current install if you want. In my experience I had to edit the entry this command created to use "linux16" to launch the ipxe environment instead of the "linux" command. This is a trivial change to the grub.cfg file.
