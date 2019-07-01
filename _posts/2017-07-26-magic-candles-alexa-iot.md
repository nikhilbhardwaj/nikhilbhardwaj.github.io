---
id: 236
title: 'Magic Candles - fun with Alexa and IoT'
date: 2017-07-26T11:39:33-04:00
author: nikhil
layout: post
guid: https://nikhilbhardwaj.in/?p=236
permalink: /2017/07/26/magic-candles-alexa-iot/
categories:
  - pi
  - Programming
  - tech tips
---
A while back my wife had picked up a packet of [flameless candles from costco.](https://www.costco.com/Mirage-5-piece-LED-Candles-The-Look-of-a-Real-Flame.product.100348013.html) These come with an infrared remote which you can change colors, switch modes between glow and flicker and schedule the candles to turn off after a predetermined time interval.

I thought it'd be cool to be able to have my Alexa controlling these, you walk into the room, turn off the lights and turn on these candles thereby creating a perfect environment for a romantic candle lit dinner. Right?

I got some time over the weekend to work on this and here it is, in all it' s glory for you to enjoy.



If you're not interested in the technical details involved in setting this up, then you can stop here. Here's the hardware that I've used &#8211;

  * Raspberry Pi (This plays a dual role, it hosts the server that communicates with the IR blaster and it's also the IoT device that Alexa talks to)
  * [Blackbean Mini](https://www.banggood.com/Broadlink-Black-Bean-Smart-Home-Wifi-Remote-IR-Controller-Universal-Appliances-Smart-Control-p-1049494.html) (This is the IR blaster, it mimics the remote)
  * Flameless Candles and Remote (For obvious reasons)

The software components are &#8211;

  * [broadlink-http-rest](https://github.com/radinsky/broadlink-http-rest) &#8211; HTTP server, running on Raspberry Pi to Communicate with the IR blaster
  * [AWS IOT SDK](https://docs.aws.amazon.com/iot/latest/developerguide/iot-sdks.html) &#8211; This is also running on my Raspberry Pi to make it an IOT device which listens on an MQTT topic to which the Alexa Skill publishes messages. This reads that message and makes a REST call to our HTTP Server
  * Alexa Skills Kit SDK &#8211; For the Alexa Skill, to publish a message to the MQTT topic
  * AWS Lambda, to host the Alexa Skill &#8211; I don't think I'll ever spin up another web server for my hobby projects

Here's a visual diagram that represents the interaction between the pieces to paint a clearer picture &#8211;

![](/assets/uploads/2017/07/MagicCandles.png)

And for those of you who want to dive deeper and play with the code, you can find it on [Github](https://github.com/nikhilbhardwaj/alexa-magic-candles).

I've also jotted down some notes and learnings based on developing this &#8211;

  * The AWS IOT suite is really good, MQTT is a secure way to interact with IOT devices. Going forward I expect to see more devices use this, the current IOT scene is quite messy with every manufacturer spinning up their own HTTP version, with base64 encoded communication which provides no security. With this you can rest assured that it wont be easy for hackers to use you IoT device for the next DDOS attack.
  * The MQTT/HTTP performance is really good, as you can see in the demo; there's no lag between my wife talking to Alexa and the action being performed, despite this going through multiple systems each running on different infrastructure and written in different languages. The IR Server Bridge is written in python, the Raspberry Pi runs the AWS IOT Javascript SDK, the Alexa skill is written in Java and is run on demand on a serverless platform.
  * REST is awesome, this build upon the previous point. This seamless integration is possible because all these pieces talk REST
  * AWS IOT SDK documentation is atrocious to the point that it almost negates all the great features that it exposes. It took me more than a few hours to read up the documentation, source code and even some [Javascript examples](https://10xnation.com/voice-control-iot-devices-alexa-voice-service/) to understand how to open a line of communication with my device using the Java SDK. This despite my familiarity with a bunch of other AWS Services. Writing good services and software isn't enough, if your users can't figure out how to use it. I hope that [my code](https://github.com/nikhilbhardwaj/alexa-magic-candles/blob/master/src/main/java/in/nikhilbhardwaj/candles/iot/AWSIOTService.java) helps someone else battling similar issues. I have a lot more to say about this, but if I was to go on, it would end up being a rant. I'll reserve that for a future post(maybe).

I had a lot of fun building this, maybe this can give someone else inspiration for their own IoT project. It's really easy to extend this to control other devices in your home &#8211; TVs, ACs, Game Consoles and a bunch of other things are all controlled with IR remotes. The IoT domain is so much fun these days, the fully automated smart home even on a budget is now a reality.
