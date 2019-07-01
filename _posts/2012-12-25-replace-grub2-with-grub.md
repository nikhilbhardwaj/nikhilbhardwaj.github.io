---
id: 189
title: Downgrade grub2 to grub
date: 2012-12-25T03:17:23-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=189
permalink: /2012/12/25/replace-grub2-with-grub/
categories:
  - Linux
  - tech tips
  - ubuntu
---
There was this weird issue that I've been facing for some time with both ubuntu 12.10 and 12.04, what happens is that my Acer Aspire One 722 netbook doesn't boot into linux at times. The first couple of times I dismissed it as a one off but that didn't stop the problem from recurring. Then I blamed my exotic grub2 setup wherein I had installed grub2 to /dev/sda5 and then was using the windows 7 bootloader to chainload it.
<!--more-->


Fed up with it I backed up my data and decided to test drive elementary os luna beta1, which is a fantastic project that is built on top of ubuntu 12.04 and after a few boot cycles the problem resurfaced. This time around I had grub2 installed to the MBR. So I began digging in for solutions and as it turns out I'm not the only one who had similar problems and found a solution which entails downgrading to grub-0.97 or grub-legacy. Most of the places you'll be advised to stick to grub2 as grub isn't maintained any more and that's a fair point but being stuck with an operating system that boots at will isn't all that fair.

I remember having used grub with older distros back in the time when there was no grub2 and it was really easy to set up and adding and removing operating system entries were a piece of cake, just add stuff to the menu.lst and viola that's it. I'm happy to report that grub still works fine as it always did, it might however not if you're running hardware that has uefi bootloaders. I followed this thread at [ubuntuforums](http://ubuntuforums.org/showthread.php?t=1298932 "Ubuntuforums") to remove grub2 and install grub.

&nbsp;

Just a word of caution, if your bootloader works fine you'd best leave it as is. playing around with bootloaders isn't for the faint-hearted. You may end up with a system that is un-bootable and before I forget, Merry Christmas to all of you!
