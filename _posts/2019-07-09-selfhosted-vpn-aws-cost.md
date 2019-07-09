---
id: 1001
title: 'Cost of Self-Hosting a VPN server in AWS'
date: 2019-07-09T15:49:03-04:00
author: nikhil
layout: post
permalink: /2019/07/09/self-hosted-vpn-aws-cost/
categories:
  - aws
  - tech tips
---
I wanted to briefly share some of the details of my self-hosted VPN setup, and to specifically talk about
the associated costs with running one in AWS.
The VPN is the central piece in my TV setup, these are the requirements that I have -
- Available app for Fire TV
- High Speed to support HD streaming
- Sever(s) shouldn't be blacklisted by popular service providers
- Easy to switch between different servers and to connect and disconnect
- Ability to exclude apps from the VPN tunnel is an added bonus.

I tried OpenVPN, IKEv2/Strongswan and Wireguard. Amongst these three Wireguard came up on top, IKEv2/Strongswan
comes at a respectable second whereas OpenVPN languishes in the last place. Now I didn't run exhaustive benchmarks
on either of these so my observations should be taken with a grain of salt. My VPN Servers were the cheapest offerings from AWS T3.nano, these boxes don't offer too much computing power and the networking stack is also
rather ordinary, however my hypothesis is that for a box to be a simple network tunnel this should be more than adequate. The speeds that I got from OpenVPN were pathetic, from the US Northeast where I live to the Asia Pacific (Bombay) region where my servers reside; were between a paltry 1 and 3 Mbps. If this was the best that was possible then I'd either need to shell out more money for a better instance on a faster network link or give up my dream.

Next I explored Strongswan and setup an IKEv2 based VPN and was pleasantly surprised at the speed boost, I now got between 5 and 8 Mbps. These aren't speeds to boast about either but for the next few months I continued to use this and was very happy with the results. The Strongswan app for Android works well on the Fire TV, the only issue was copying the self signed Server Certificate onto the Fire Stick and then importing them into the Strongswan app.
While I was happy with my Strongswan setup, I wasn't delighted with the app. Debugging connection errors were a huge pain and moving from one server that I accidentally nuked was laborious.

A couple of months ago, I read about Wireguard which is a new VPN protocol that is under heavy development. It's not wery well tested and doesn't offer any crypto guarantees (yet). This normally would be a red flag but they tout exceptional speeds when compared to the competition and for my current usecase just masking my IP address is adequate. You should carefully evaluate any VPN product to understand what the underlying protocol is and what guarantees it makes if any. The things that I loved about Wireguard are
- Ease of setup, it took me some time to grok what the high level idea was, afterwards setup has been a breeze
- Cross platform support, specially for a new tool. It works well on Linux, MacOs, iOS and Android with support for Windows (which I have not tested)
- Ease of configuration options, I love that I can simply share a QR code with my friends and they're setup by just scanning that. The configuration on a Fire TV was somewhat harder due to mixed case encryption keys needing to be typed in with the Fire TV remote but I soon realized the futility of this approach and used adb like any sane person would.
- Lastly the best thing was the speeds, with Wireguard I consistently get speeds between 13-15 Mbps.

Now with the VPN protocol comparision out of the way, lets actually talk about what it costs to run a VPN server in AWS.
AWS offers multiple products and it is critically important to understand their cost structure and to then use this optimally.

Here's my bill from the last month -

<object data="/assets/uploads/2019/07/09/Aws-Bill-Jun2019.pdf" width="1000" height="1000" type='application/pdf' />

Now you can see that it was costing me about $28 a month, this is split at about $5 for the monthly cost to run the server and the remainder for the 200GB data transfer costs. I have some alexa promotional credits that covered these costs but these costs are unacceptable when compared to the multiple VPN providers which provide servers in multiple regions and a much larger bandwidth allowance.

The cost for the server cost was so high because to get started I was using on-demand instances which are typically the highest prices, they also offer the most flexibility but since I needed to run the server all the time. I could bring down this cost to $1.5 a month by using reserved capacity and commiting to paying for 3 years upfront.

The server cost as you can see is a fraction of the overall cost, the lions share here is the data transfer cost. There's no easy way for me to reduce the data transfer costs. Wireguard supports excluding certain apps from the VPN connection, so excluding Netflix will save me some of the bandwidth. The fix for this problem was to actually use another offering, if you're familiar with VPS, then you'd know that providers like Digital Ocean price their droplets starting from $5 a month. This bundle includes a server along with a generous allowance. As it turns out, AWS too offers a VPS service called LightSail this offers multiple packages but for our usecase the two basic packages are adequate the $3.50 and the $5. Along with a 1TB bandwidth allowance, comparable speeds to the T3.nano family, they also offer a static IP and DNS hosting. All in all this makes for a very compelling package, I get predictable cost and performance at a fraction 1/5th of the initial cost.

Hope this helps you if you're trying to host your own VPN server in AWS or another Cloud Provider. A couple of things to keep in mind are understanding the cost structure and the different pricing models and to stay upto date with the newest offerings. The rate at which AWS spins up new offerings is quite frankly astonishing, while it's nearly impossible to know about each of their services you can use forums like r/aws to ask people what they're using for something similar.

In the upcoming posts, I'll share some more details of my TV setup, the highlight being able to mirror whatever is on my TV anywhere with either RTMP and HLS. Stay tuned.
