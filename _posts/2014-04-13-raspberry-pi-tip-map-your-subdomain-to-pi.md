---
id: 213
title: 'Raspberry Pi tip : Map your Subdomain to Pi'
date: 2014-04-13T21:57:25-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=213
permalink: /2014/04/13/raspberry-pi-tip-map-your-subdomain-to-pi/
categories:
  - Linux
  - pi
---
After I had my Raspberry Pi setup, I wanted to create a subdomain which would point to it.
This is trivial to set up if you have a static IP but I&#8217;m assuming that like me you don&#8217;t have that.

The way that I have set this up is by following [this](http://superuser.com/questions/127807/how-can-i-route-a-domain-to-my-box-at-home) excellent post on superuser. First you need to set up a dynamic dns for your pi. I use [DNSDynamic](http://www.dnsdynamic.org/) for this, a tutorial on how to set this up for your pi can be found [here](http://blog.mivia.dk/free-dynamic-dns-for-raspberry-pi/). With dynamic dns set up, it&#8217;s like having a static ip.

All you need to do after this is to create a CNAME record which points to your dynamic dns. This can be created using your domain registrar&#8217;s web interface. A CNAME is basically a pointer and can point to any IP or domain. In my case I set up pi.nikhilbhardwaj.in to point to my dynamic dns. If you&#8217;ve set that up correctly you can use dig to verify this. Here&#8217;s what I get, babypi.ssh22.net is my dynamic dns. I&#8217;d advice you to choose a better name!

After this it&#8217;s a matter of forwarding the right ports on your home router and viola you have a subdomain that points to your pi!

    dig pi.nikhilbhardwaj.in

    ; <<>> DiG 9.8.3-P1 <<>> pi.nikhilbhardwaj.in
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 57260
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 2, ADDITIONAL: 4

    ;; QUESTION SECTION:
    ;pi.nikhilbhardwaj.in.      IN  A

    ;; ANSWER SECTION:
    pi.nikhilbhardwaj.in.   13171   IN  CNAME   babypi.ssh22.net.
    babypi.ssh22.net.   60  IN  A   106.51.135.186
