---
id: 170
title: gprs and wvdial over bluetooth
date: 2012-10-01T20:51:13-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=170
permalink: /2012/10/01/gprs-and-wvdial-over-bluetooth/
categories:
  - Linux
  - tech tips
---
I must say that the network manager handles ppp connections rather poorly, sometimes they work but most of the times they don&#8217;t. The situation is worse still with mobile phones, I have a nokia series 40 mobile phone and when my mts subscription expires, I need to use it for a couple of days. I&#8217;ll walk you through the steps that allowed me to connect to the internet using my tata docomo gprs connection over bluetooth.

<!--more-->Before getting started, your gprs should be configured on the mobile device, i.e. you should be able to access internet on that. This typically requires you to set up the correct access point for tata docomo 2G connections it is tata.docomo.internet, you can get this from your provider. Also switch on your bluetooth, the first thing we need is the device MAC address.

<pre class="brush: plain; title: ; notranslate" title="">➜  ~  sudo hcitool scan
Scanning ...
B0:5C:E5:48:5B:B4       X2-01

</pre>

We also need to find the channel with

<pre class="brush: plain; title: ; notranslate" title="">[root@lovelock ~]# sdptool search dun
Inquiring ...
Searching for dun on B0:5C:E5:48:5B:B4 ...
Service Name: Dial-up networking
Service RecHandle: 0x10003
Service Class ID List:
  "Dialup Networking" (0x1103)
  "Generic Networking" (0x1201)
Protocol Descriptor List:
  "L2CAP" (0x0100)
  "RFCOMM" (0x0003)
    Channel: 1
Language Base Attr List:
  code_ISO639: 0x656e
  encoding:    0x6a
  base_offset: 0x100
Profile Descriptor List:
  "Dialup Networking" (0x1103)
    Version: 0x0100
</pre>

Look for channel in the output, in my case the channel is 1.

Next we need to bind it to a device in our case it shall be /dev/rfcomm0. In the command below you can see 0 refers to the device we want to bind to followed by the MAC address and the channel. Be sure to substitute your channel value here if it is different.

<pre class="brush: plain; title: ; notranslate" title="">sudo rfcomm bind 0 B0:5C:E5:48:5B:B4 1
sudo rfcomm
    rfcomm0: B0:5C:E5:48:5B:B4 channel 1 clean
</pre>

Now that the device is all set up, we need an entry in /etc/wvdial.conf

<pre class="brush: plain; title: ; notranslate" title="">[Dialer nokia]
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0
Init3 = AT
Modem = /dev/rfcomm0
Phone = *99#
ISDN = no
Baud = 115200
Stupid Mode = yes
Carrier Check = no
Username = PHONE_NO
Password = anything
</pre>

You might need to replace the username with your phone no and the password can be anything, for prepaid connections they aren&#8217;t checked as far as I know. Now just dial this connection and you&#8217;ll be ready to roll!

<pre class="brush: plain; title: ; notranslate" title="">sudo wvdial nokia
--&gt; WvDial: Internet dialer version 1.61
--&gt; Sending: AT
AT+GCAP
+GCAP: +CGSM,+W
OK
--&gt; Modem initialized.
--&gt; Sending: ATDT*99#
--&gt; Waiting for carrier.
CONNECT
--&gt; Carrier detected.  Starting PPP immediately.
--&gt; Starting pppd at Mon Oct  1 08:32:04 2012
--&gt; Pid of pppd: 2223
--&gt; Using interface ppp0
--&gt; local  IP address 14.194.77.191
--&gt; remote IP address 0.194.77.191
--&gt; primary   DNS address 121.242.190.210
--&gt; secondary DNS address 121.242.190.181

</pre>

Now for use subsequently you needn&#8217;t repeat all the steps, here are the two that you need to execute (you could make a shell script for this too also you&#8217;ll need to run them with root privileges)

<pre class="brush: plain; title: ; notranslate" title="">rfcomm bind 0 B0:5C:E5:48:5B:B4 1
wvdial nokia
</pre>

And that&#8217;s how you can use your phone&#8217;s gprs/3G connection on linux. Let me know in the comments if you find this useful or have any queries.
