---
id: 185
title: Keep Windows and Linux time in sync
date: 2012-12-13T23:56:02-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=185
permalink: /2012/12/13/windows-linux-time-sync/
categories:
  - Linux
  - tech tips
  - ubuntu
---
Every time I log into windows after having used linux on my netbook there is a problem with the system time. It is because linux treats the time set in your BIOS clock to use the UTC clock, this is a problem as windows treats it to be set to your local time. If you're using only one OS then both of these choices are acceptable design choices but when you use it becomes a problem. When I'm online it's not a problem as both windows and linux sync their times with the internet but when offline it's irritating to look at the clock and see a time that makes no sense.

Fortunately you can tell linux to follows the convention that windows follows, telling windows to behave like linux on the other hand is significantly harder. The best thing about linux is that it makes it's assumptions and lets you change them to suit your preference. We need to edit this file _/etc/default/rcS _for ubuntu 12.10

<pre class="brush: plain; title: ; notranslate" title=""># assume that the BIOS clock is set to UTC time (recommended)
UTC=no

</pre>

By default the option is yes but we need to change it to no and from the next reboot the problem is solved!
