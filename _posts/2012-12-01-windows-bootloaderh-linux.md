---
id: 176
title: Using the Windows 7/8 bootloader to dual boot linux
date: 2012-12-01T13:04:12-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=176
permalink: /2012/12/01/windows-bootloaderh-linux/
categories:
  - Linux
  - tech tips
  - ubuntu
---
In the past whenever I had to install linux along with windows I would install grub and it works flawlessly most of the time. Sometimes however when you&#8217;re experimenting with something unusual, it is handy to know how to load linux using the windows bootloader. I used it when I was transferring my ubuntu installation from my laptop to my netbook.
<!--more-->


By default grub is installed to the MBR, it overwrites the windows bootloader. On one hard disk there can only be one bootloader that resides in the MBR, the trick is to install grub to a partition, then make an image of that and use it to boot into linux. It sounds slightly tricky so I&#8217;ve mentioned the exact steps.

First we need to install grub to a partition, this can be done by

<pre class="brush: plain; title: ; notranslate" title="">grub-install --force /dev/sda5</pre>

you need to replace sda5 with the appropriate partition for your setup.

Next we need to save the grub image

<pre class="brush: plain; title: ; notranslate" title="">dd if=/dev/sda5 of=linux.bin bs=512 count=1</pre>

this linux.bin that gets created needs to be copied to your C drive.

Finally we need to add an entry into the windows bootloader, that can be done using

<pre class="brush: plain; title: ; notranslate" title="">bcdedit /create /d “Linux” /application BOOTSECTOR
It will return an id which looks like {asdasd-98as-asdasd}
this has to be used with the subsequent commands
bcdedit /set {ID} device partition=c:
bcdedit /set {ID}  path \linux.bin
bcdedit /displayorder {ID} /addlast
bcdedit /timeout 5</pre>

Next time you reboot you will get a choice to boot into either windows or linux.
