---
id: 117
title: Installing ubuntu to a usb drive using vmware
date: 2012-06-25T22:35:47-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=117
permalink: /2012/06/25/installing-ubuntu-to-a-usb-drive-using-vmware/
categories:
  - Linux
  - tech tips
  - ubuntu
---
In this post I’m going to walk you through installing ubuntu on a usb drive using vmware, that can boot any system not only virtual machines also we’ll create an ntfs/fat32 partition so that we can use it with windows computers as an ordinary pen drive too.

The first step is to partition the pendrive, I have a 16 GB device and I’ll use half of it for the linux installation and the other half for data. We can use either gparted or cfdisk from the live cd to do this. Another important thing to note is that for any usb storage device, it’s life is affected more by the number of writes that reads. So we’ll also tune a few parameters after the installation to maximize the life of the usb drive.

[<img style="background-image: none; border-right-width: 0px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="Partitioned USB drive - VMware Player_2012-06-25_16-10-56" border="0" alt="Partitioned USB drive - VMware Player_2012-06-25_16-10-56" src="http://nikhilbhardwaj.in/wp-content/uploads/2012/06/Partitioned-USB-drive-VMware-Player_2012-06-25_16-10-56_thumb.png" width="244" height="199" />](http://nikhilbhardwaj.in/wp-content/uploads/2012/06/Partitioned-USB-drive-VMware-Player_2012-06-25_16-10-56.png)

Once the device is partitioned correctly we can install ubuntu as we would on an ordinary hard drive be sure to install the boot loader to the usb drive too. Don’t create any swap partition during the installation that will literally kill your usb drive because it continuously writes data to and from the swap.
Also, having a swap partition on a usb drive doesn’t make too much sense. There is no way you can compare the performance of the RAM to a cheap usb disk.

Once you are done with it, you have successfully installed ubuntu to a usb drive, you can use this to boot any computer. Your OS form now will be in your pocket but I’ll mention a few tips that will make your performance slightly better by using the usb drive more efficiently. Linux keeps a track of the timestamps when files are accessed, this involves writing data to the disk whenever a file is used on a usb drive this is something we don’t need. You can disable this using the noatime option in /etc/fstab. Also we shouldn’t keep update the systemeach time a tiny update is released and ther is no benefit of caching the packages or letting ubuntu install multiple kernels. It may also help to use cinnamon, I have described how that can be used in an earlier blog post. Another thing is that you shouldn’t install restricted drivers or vmware tools as they will create a problem when you boot on machines where that specific piece of hardware isn’t present.

To summarize, keep the usb install lean and mean, you can install the gcc compilers and configure vim and you now have a world class OS in your pocket to use anywhere you want. Let me know how your install went and feel free to ask if you have any doubts in the comments. 
