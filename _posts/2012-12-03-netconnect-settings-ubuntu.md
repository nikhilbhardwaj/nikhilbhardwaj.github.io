---
id: 180
title: Reliance Netconnect+ Settings for Ubuntu
date: 2012-12-03T16:09:04-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=180
permalink: /2012/12/03/netconnect-settings-ubuntu/
categories:
  - Linux
  - tech tips
  - ubuntu
---
I had written a post on how we can easily get MTS Mblaze to work under linux and as it turns out, the Reliance Netconnect+ is equally easy to set up and use. Instead of repeating the entire procedure which I have already mentioned here, I&#8217;ll just post the relevant wvdial configuration file. You need to add the following snippet to your /etc/wvdial.conf

<pre>[Dialer netconnect]
New PPPD = yes
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0
Modem Type = USB Modem
Baud = 460800
New PPPD = yes
Modem = /dev/ttyUSB0
ISDN = 0
Username = 9388******
Password = 9388******
Phone = #777
Stupid Mode = 1
</pre>

It goes without saying that you need to replace the username and password with your netconnect phone no. To connect simply type this in a terminal

<pre>sudo wvdial netconnect</pre>

Here&#8217;s what I get

<pre>➜  ~  sudo wvdial netconnect
--> WvDial: Internet dialer version 1.61
--> Initializing modem. --> Sending: ATZ OK
--> Sending: ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0 ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0 OK
--> Modem initialized.
--> Sending: ATDT#777
--> Waiting for carrier. ATDT#777 CONNECT 3100000
--> Carrier detected.  Starting PPP immediately.
--> Starting pppd at Mon Dec  3 15:45:39 2012
--> Pid of pppd: 3981
--> Using interface ppp0
--> local  IP address 115.242.128.198
--> remote IP address 220.224.141.145
--> primary   DNS address 220.226.6.104
--> secondary DNS address 220.226.100.40
 </pre>

Happy browsing with Reliance Netconnect+, I suspect that the MTS device and the Reliance device are actually identical, the only difference being the firmware. As usual let me know in the comments if this helped or if you have some clarifications.
