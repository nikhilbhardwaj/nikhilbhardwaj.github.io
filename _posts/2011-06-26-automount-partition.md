---
id: 14
title: Automatically Mount Partitions at Boot Up
date: 2011-06-26T15:15:16-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=14
permalink: /2011/06/26/automount-partition/
categories:
  - Linux
  - Sabayon
tags:
  - fstab
  - linux
---
I dual boot windows and linux and what happens is that most of my data resides on an ntfs volume which can be accessed by both the operating systems. It's really simple to mount this volume, all that needs to be done is that you click it in the file manager and depending on your distro you may or may not be prompted for the administrator password. This system works well but its not very convenient. I generally configure my distro to automatically mount some partitions at boot up, that way i can easily create symbolic links  that span across volumes and make it easier to access files.<!--more-->

This is a relatively simple process, it requires the use of the shell and a text editor of your choice, I swear by <a href="http://www.vim.org" target="_blank">gvim</a> which is an improved version of the legendary <a href="http://en.wikipedia.org/wiki/Vi" target="_blank">vi</a> editor, I like it so much that i use it in windows too but with all things linux there is a steep learning curve with this so beginners would be better off using a more forgiving editor like <a href="http://www.nano-editor.org/" target="_blank">nano</a> or <a href="http://www.kde.org/applications/utilities/kwrite" target="_blank">kwrite</a>/<a href="http://www.gedit.org" target="_blank">gedit</a> depending on the desktop environment that you choose.

First we need to determine the name of the partition that we want mounted automatically. To do this log into a terminal window as the root user and run fdisk.

<pre class="brush: bash; title: ; notranslate" title="">nikhil@lovelock ~ $ su -
Password:
lovelock ~ # fdisk -l

Disk /dev/sda: 500.1 GB, 500107862016 bytes
255 heads, 63 sectors/track, 60801 cylinders, total 976773168 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0xe7019cea

Device Boot      Start         End      Blocks   Id  System
/dev/sda1            2048    27265023    13631488   27  Unknown
/dev/sda2   *    27265024    27469823      102400    7  HPFS/NTFS
/dev/sda3        27469824   238415871   105473024    7  HPFS/NTFS
/dev/sda4       238420726   976768064   369173669+   5  Extended
/dev/sda5       238420728   867991949   314785611    7  HPFS/NTFS
/dev/sda6       867992013   972591164    52299576   83  Linux
/dev/sda7       972591228   976768064     2088418+  82  Linux swap / Solaris
</pre>

In my case I want to mount the partition named **/dev/sda5** . In case this is mounted we should un-mount it and then create a mount point for this.

<pre class="brush: bash; title: ; notranslate" title="">lovelock ~ # umount /dev/sda5
lovelock ~ # mkdir /media/Data
</pre>

Now We'd want to be able to find out our user id and group id, this can be found out by

<pre class="brush: bash; title: ; notranslate" title="">lovelock ~ # grep nikhil /etc/passwd
nikhil:x:1000:1001:nikhil bhardwaj:/home/nikhil:/bin/bash
</pre>

You can substitute nikhil with your won user name. With this we can see that the user id is 1000 and group id is 1001.
Now we can add the entry for this partition in our <a href="http://linux.die.net/man/5/fstab" target="_blank">fstab</a>. Any text editor can be used for this. Do not change any of the existing data in the **/etc/fstab**. Add an entry as I've done below.

<pre class="brush: bash; title: ; notranslate" title="">lovelock ~ # cat /etc/fstab
# /etc/fstab
# Created by anaconda on Sun Jun 26 12:23:54 2011
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=147174a0-c3db-4e59-acbf-c2c32126ea4a /                       ext4    defaults        1 1
UUID=53e54249-1672-45d6-b337-c4750b8ceff5 swap                    swap    defaults        0 0
tmpfs                   /dev/shm                tmpfs   defaults        0 0
devpts                  /dev/pts                devpts  gid=5,mode=620  0 0
sysfs                   /sys                    sysfs   defaults        0 0
proc                    /proc                   proc    defaults        0 0
#Custom entry for data partition
/dev/sda5 /media/Data ntfs-3g uid=1000,gid=1001,fmask=0111,dmask=0000 0  0
</pre>

If we have invalid entries in the <a href="http://linux.die.net/man/5/fstab" target="_blank">fstab</a> then the computer will not boot up. To check if we got it right run.

<pre class="brush: bash; title: ; notranslate" title="">lovelock ~ # mount -a
</pre>

Voila! You are almost done, this will work fine but you'll notice that the other lines start with a UUID. This is useful in case you have multiple hard disks on your computer. Even if the device name changes on the addition of new hardware the UUID remains constant.
Lets find out the UUID of the partition and make the final change to the <a href="http://linux.die.net/man/5/fstab" target="_blank">fstab</a>.

<pre class="brush: bash; title: ; notranslate" title="">lovelock ~ # blkid
/dev/sda1: LABEL="PQSERVICE" UUID="924491054490ED6B" TYPE="ntfs"
/dev/sda2: LABEL="SYSTEM RESERVED" UUID="C0A89163A89158AC" TYPE="ntfs"
/dev/sda3: LABEL="Acer" UUID="74A09312A092DA46" TYPE="ntfs"
/dev/sda5: UUID="74EC9395EC934FEA" TYPE="ntfs"
/dev/sda6: UUID="147174a0-c3db-4e59-acbf-c2c32126ea4a" TYPE="ext4"
/dev/sda7: UUID="53e54249-1672-45d6-b337-c4750b8ceff5" TYPE="swap"
</pre>

The new <a href="http://linux.die.net/man/5/fstab" target="_blank">fstab</a> line for my system would be:

<pre class="brush: bash; title: ; notranslate" title="">#Custom entry for data partition
UUID=74EC9395EC934FEA /media/Data ntfs-3g uid=1000,gid=1001,fmask=0111,dmask=0000 0  0
</pre>

That's it for the auto mounting part.

Let me demonstrate a use for it too. Here's what I do.

<pre class="brush: bash; title: ; notranslate" title="">nikhil@lovelock ~ $ ln -s /media/Data/Music/
nikhil@lovelock ~ $ ln -s /media/Data/Videos/
nikhil@lovelock ~ $ ln -s /media/Data/Movies/ Videos/
nikhil@lovelock ~ $ ls -l
total 20
drwxr-xr-x  2 nikhil nikhil 4096 Jun 26 12:34 Desktop
drwxr-xr-x  9 nikhil nikhil 4096 Jun 26 11:51 Documents
drwxr-xr-x  2 nikhil nikhil 4096 Jun 21 18:38 Downloads
drwxr-xr-x  6 nikhil nikhil 4096 Jun 26 11:41 Dropbox
lrwxrwxrwx  1 nikhil nikhil   18 Jun 26 14:51 Music -&gt; /media/Data/Music/
drwxr-xr-x 10 nikhil nikhil 4096 Jun 26 14:07 Sources
lrwxrwxrwx  1 nikhil nikhil   19 Jun 26 14:51 Videos -&gt; /media/Data/Videos/
</pre>

This way I can access the Music and Videos as if they were inside my home drive itself. This is because symbolic links can span across various volumes whereas hard links can't.
I hope you found it informative and useful.
