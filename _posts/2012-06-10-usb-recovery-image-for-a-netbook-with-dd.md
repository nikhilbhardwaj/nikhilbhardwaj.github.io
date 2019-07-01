---
id: 108
title: Creating a usb recovery image for a netbook using dd
date: 2012-06-10T16:05:29-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=108
permalink: /2012/06/10/usb-recovery-image-for-a-netbook-with-dd/
categories:
  - Linux
  - tech tips
tags:
  - dd
  - linux
  - recovery
---
Yesterday I got my new shiny <a title="Acer netbook details on amazon" href="http://www.amazon.com/Acer-AO722-BZ454-11-6-Inch-Netbook-Espresso/dp/B004UR16ES" target="_blank">Acer aspire one 722 netbook</a>, it comes with windows 7 starter and I'm not going to stick with it for long but before I start with my experiments I thought of creating a recovery image for it. Having one is particularly useful if things go wrong and you want to use Acer's warranty, trust me it's a pain in the rear to explain to the customer support that you use linux or another operating system. Fortunately acer ships with Acer E Recovery Management which is an excellent utility to create a startup disk. I used my USB drive to create a restore disk and also to store my drivers. The only problem is that it took a total of about 12GB out of the 16GB available on my USB drive. I keep using the pendrive for other things too so this couldn't be a permanent solution.<!--more-->In comes

<a title="Disk Dump" href="http://en.wikipedia.org/wiki/Dd_(Unix)" target="_blank">dd, </a>this is a program that can clone disk's exactly. I'll show you how we can use this to create an image and store it on an external hard drive and to restore it back to the pendrive in case it is required again, I do these on my main laptop's using ubuntu 12.04 but you can use any linux distribution or a live cd for this. dd is also available for windows but I haven't used it too much inside windows so I can't guarantee it's working.

First open a root shell and plug in your USB drive

<pre class="brush: plain; title: ; notranslate" title=""># fdisk -l

Disk /dev/sda: 500.1 GB, 500107862016 bytes
255 heads, 63 sectors/track, 60801 cylinders, total 976773168 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2bd2c32a

Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048   362371071   181184512    7  HPFS/NTFS/exFAT
/dev/sda2       362371072   467228671    52428800   83  Linux
/dev/sda3       467228672   488200191    10485760   83  Linux
/dev/sda4       488200192   976773119   244286464    5  Extended
/dev/sda5       488202240   976773119   244285440    7  HPFS/NTFS/exFAT

Disk /dev/sdc: 16.0 GB, 16001269760 bytes
255 heads, 63 sectors/track, 1945 cylinders, total 31252480 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xa18b44c7

Device Boot      Start         End      Blocks   Id  System
/dev/sdc1   *          63    31252479    15626208+   7  HPFS/NTFS/exFAT

</pre>

The last few lines are of interest to us, the identifier for my drive is /dev/sdc this will be different for you make a note of this, we'll need this later.

<pre class="brush: plain; title: ; notranslate" title=""># dd if=/dev/sdc | gzip &gt; /home/nikhil/Downloads/netbook-recovery.gz

</pre>

You should make changes to the path's as necessary, It'll take some time to finish executing once it does you'll have your image that you can store someplace safe.

Now you can format the USB drive and use it normally. If and when you want to restore this image back to the usb, you'll need to run the following command.

<pre class="brush: plain; title: ; notranslate" title=""># gzip -dc /home/nikhil/Downloads/netbook-recovery.gz | dd of=/dev/sdc

</pre>

A word of warning, dd is a dangerous command if you get your drive paths wrong it will overwrite your hard drive and destroy existing partitions before blindly copying and pating these command please understand the commands and only then should you execute them.

You can use this tool to create iso images from cds or dvds and also to back up your partitions also you can create virtual disk images which are similar to those used by virtualization software like vmware and VirtualBox. Sometime soon I'll also write a post on how to use a swap file in linux and also on how to encrypt sensitive data.
