---
id: 160
title: Kde4 map windows key to kickoff launcher
date: 2012-09-09T20:02:02-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=160
permalink: /2012/09/09/kde4-map-windows-key-to-kickoff-launcher/
categories:
  - arch
  - Linux
  - Random
  - Sabayon
---
KDE's equivalent to the windows start menu is the kickoff launcher, being a windows user for a long time before I moved to linux some habits just don't go away. I tried to change the shortcut key associated to kickoff but as it turns out, KDE treats the Win Key as a meta key. That basically means that just like the Shift, Control and the Alt keys it too has no meaning on its own and must be paired with another key to perform some useful function.

<!--more-->

Nevertheless, it's not too hard to achieve the mapping that I had in mind. We need to create an executable file in the ~/.kde4/Autostart directory with the following contents.

<pre class="brush: plain; title: ; notranslate" title="">#!/bin/bash
# Win Key to F13, to launch the start menu
xmodmap -e 'keycode 133=F13'
</pre>

Once we source this file or logout and login again then we can change the keyboard shortcut to use only the Win Key. What has happened is that we have mapped the Win Key to a virtual key F13 which is no longer a meta key.

I discovered this tip sometime back in some KDE forums, thought I'd share it here so that I could find it easily next time I install KDE on somebody's laptop.
