---
id: 215
title: Setting up raspberry pi
date: 2014-04-13T22:54:02-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=215
permalink: /2014/04/13/setting-up-raspberry-pi/
categories:
  - Linux
  - pi
---
Here&#8217;s a list of things I do to set up my raspberry pi and a small note, the purpose of this list is to help me remember what all I need to setup if and when I start from scratch the next time around.

1. Finding your pi&#8217;s IP on the [local network](http://raspberrypi.stackexchange.com/questions/13936/find-raspberry-pi-address-on-local-network)!

I don&#8217;t have a dedicated monitor and run my pi headless. I used to do this by running a for loop and finding the ips of all my devices on the local network and then sshing into them until I found my pi but this is easier and um.., more scientific!

2. Setup Vim and fish on pi.

I don&#8217;t like editing files with nano and so setting up Vim is essential and fish is an awesome replacement to bash/zsh you may want to give it a spin. It&#8217;s history management is way better than ohmyzsh.

3. Setup [Avahi](http://www.howtogeek.com/167190/how-and-why-to-assign-the-.local-domain-to-your-raspberry-pi/) or Zeroconf

It&#8217;s always easier to remember hostnames than it is to remember ips and this is where Avahi shines. Now I can access my pi with pi.local even if it&#8217;s local ip changes.

4. Remove [Xorg](http://raspberrypi.stackexchange.com/questions/4745/how-to-uninstall-x-server-and-desktop-manager-when-running-as-headless-server) and the desktop packages

I like to run my pi, lean and mean there is no need for the desktop when I run it headless, this saves both the disk space and data with updates

5. Setup a [bittorrent](http://www.howtogeek.com/142044/how-to-turn-a-raspberry-pi-into-an-always-on-bittorrent-box/) web client

The folks at howtogeek have an excellent tutorial on setting up deluge, there are a couple of other alternatives as well but deluge works for me quite well.

6. Give your pi a [public ip/domain](http://blog.mivia.dk/free-dynamic-dns-for-raspberry-pi/)

What good is your pi if you can only access it over the local internet. The whole point of setting up a bittorrent web ui was to be able to download stuff remotely and watch it after you get home. You can also point your subdomain to your pi as I did in my last post.

7. Set up your external hard drive and [samba](http://theurbanpenguin.com/wp/?p=2415) to share it over the network.

To watch the TV shows or movies that you downloaded on your pc/mac you need to set up samba and also to connect your external hard drive to pi. Connecting the external hard drive is the same as connecting to any other linux box and so I&#8217;m omitting the steps here.

I&#8217;ll probably add more stuff here in time but this is my barebones pi setup.
