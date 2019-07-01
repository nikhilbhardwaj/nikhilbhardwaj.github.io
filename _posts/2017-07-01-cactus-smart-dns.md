---
id: 239
title: Smart DNS to sidestep geolocation checks
date: 2017-07-01T21:40:44-04:00
author: nikhil
layout: post
guid: https://nikhilbhardwaj.in/?p=239
permalink: /2017/07/01/cactus-smart-dns/
categories:
  - Random
  - tech tips
---
One of the HDMI ports of my TV is powered by Raspberry Pi, I use this to stream content that isn't available in my current geography. The most obvious way to bypass geo-restrictions is to use a VPN, these are great in theory but a high performance VPN provider is hard to find and quite expensive as well.

Recently I discovered that [Smart DNS](https://en.wikipedia.org/wiki/Smart_DNS_proxy_server) is an alternative to VPNs, this is a very clever implementation, which intercepts only a small portion of the traffic that corresponds to the geolocation checks.

I tried out [CactusVPN](https://www.cactusvpn.com/free-smart-dns/), they're one of the rare providers that provide a truly free service. Shout out to you guys at [CactusVPN](https://www.cactusvpn.com/free-smart-dns-trial/), I was able to set this up easily on both my mobile devices as well as the raspberry pi, they have apps for all major platforms/oses(Windows, macOS, Android and iOS) as well as documentation for setting up DNS on linux; which is really nice! The DNS service is available for locales like US, Canada, UK, Germany, Poland and Sweden. Here's a [list of websites](https://www.cactusvpn.com/smart-dns/unblocked-websites/) that can be unblocked using their services. I hope that they expand their services into other regions as well &#8211; India would be swell!

If you want more control, then you could setup your own Smart DNS server in the cloud. [Netflix-Proxy](https://github.com/ab77/netflix-proxy) looks really promising and I'm going to set it up in India to see if I can unblock Hotstar.

Do note that Smart DNS may not be the best solution for the more adventurous who use P2P, in those cases VPN may be better. But Smart DNS works great for cases where you want to access freely available content or content that you actually pay for and are traveling or are locked out due to poorly implemented checks.

Do let me know if you know of other Smart DNS providers, I'd love to take them out for a spin(specially if they have Indian endpoints)
