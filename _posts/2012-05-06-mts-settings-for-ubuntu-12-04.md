---
id: 95
title: MTS Settings for Ubuntu 12.04
date: 2012-05-06T19:02:51-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=95
permalink: /2012/05/06/mts-settings-for-ubuntu-12-04/
categories:
  - Linux
  - tech tips
---
I switched to ubuntu after the new LTS release and was having some problems with my MTS Mblaze connection. Sometime&#8217;s it&#8217;d work and sometimes it wouldn&#8217;t. There seems to be a bug in modem-manager which constantly keeps crashing so I decided to use wvdial instead. We need to install the wvdial package

<pre>sudo apt-get install wvdial</pre>

and then create the file /etc/wvdial.conf

<pre>[Dialer mts]
Stupid Mode = 1
Inherits = Modem0
Password = mts
Username = internet@internet.mtsindia.in
Phone = #777
[Modem0]
Init1 = ATZ
SetVolume = 0
Modem = /dev/ttyUSB0
Baud = 115200
FlowControl = Hardware (CRTSCTS)
Dial Command = ATDT </pre>

Then we can connect to the internet using

<pre>sudo wvdial mts</pre>

This is the output that I get when the dialer is run. Occasionally it will have some problems you can just disconnect and try again.

<pre>--> WvDial: Internet dialer version 1.61
--> Initializing modem.
--> Sending: ATZ OK
--> Modem initialized.
--> Sending: ATDT#777
--> Waiting for carrier. ATDT#777 CONNECT 3100000
--> Carrier detected.  Starting PPP immediately.
--> Starting pppd at Sun May  6 18:35:05 2012
--> Pid of pppd: 7231
--> Using interface ppp0
--> local  IP address 116.202.159.156
--> remote IP address 10.228.138.131
--> primary   DNS address 10.228.129.114
--> secondary DNS address 10.228.129.113 </pre>
