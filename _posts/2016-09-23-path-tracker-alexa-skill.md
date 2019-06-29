---
id: 232
title: Path Tracker an Alexa Skill for local train timings
date: 2016-09-23T09:00:02-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=232
permalink: /2016/09/23/path-tracker-alexa-skill/
categories:
  - Programming
---
I&#8217;ve had the Amazon Echo for a while, recently I had some time on my hands and decided to build a skill that at least I would find useful.

Typically my wife and I talk with Alexa to ask her for the weather, we use it to set timers when doing the laundry or short term reminders and occasionally to play music or audiobooks.

Before leaving home for office, my wife and I generally check the public transit timings. I thought it&#8217;d be cool if Alexa could tell us that instead, with this in mind I searched around for PATH schedules and how to access that information programatically. Turns out the Port Authority have this [available to developers](http://www.panynj.gov/path/developers.html) in the [GTFS](https://developers.google.com/transit/gtfs/) . After reading the [GTFS Reference](https://developers.google.com/transit/gtfs/reference/) and playing around with the PATH feed it took me a couple of hours to wrap my head around and to come up with a simple way to find train timings between any two stations.

After I had a working version of the train timings algorithm coded, I proceeded to read the documentation for the Alexa skills programming model, the documentation is a little dry but starts making sense as you code up and test your skill. I found the [Big Nerd Ranch youtube videos](https://www.youtube.com/channel/UCbx0SPpWT6yB7_yY_ik7pmg) to be very helpful in getting a general feel of the programming model.

I had initially planned to host the backend as a service on one of my raspberry pi&#8217;s but due to the number of hoops that Amazon makes you jump through, I ended up leaning towards AWS lambda. It was a bit of a pain to get started with lambda as the support community is rather limited, you&#8217;ll need to figure out some of the things yourself by trial and error. (I had no luck at [AWS forums](https://forums.aws.amazon.com/thread.jspa?threadID=238933) and very little at StackOverflow, overall though StackOverflow seems to be a much better place to ask your questions and get some help)

Once you overcome the initial challenges with running your skill on AWS lambda, it&#8217;s actually a fun platform to develop on, I was no fan going into this but came out a believer the Zero Infrastructure and configuration to host code is certainly going to catch on. I do have some complaints about performance during a cold start but I reckon that this is only going to get better with time.

After everything was done and I had tested the functionality with my local echo device, I submitted the skill for certification.
A few days later I heard back from the certification team that my skill was rejected. I got this response

> <p style="padding-left: 30px;">
>   Issues with skill in English (US)
> </p>
>
> <p style="padding-left: 30px;">
>   1. When attempting to invoke the skill with your second and third example phrases, the skill fails to recognize the phrases. The example phrases must function without error since these are interactions that users are most likely to try. Please see test case 3.1 from our Submission Checklist for guidance on example phrases.
> </p>
>
> <p style="padding-left: 30px;">
>   Example:
> </p>
>
> <p style="padding-left: 30px;">
>   User: “Alexa Ask Path Tracker When is the next train between Exchange Place and Newark”/ “Alexa Ask Path Tracker Train to Exchange Place from Newark”
> </p>
>
> <p style="padding-left: 30px;">
>   The skill fails to recognize the phrases.
> </p>

I spent an hour or so trying to figure out why the skill won&#8217;t recognize the phrase and came to a conclusion that maybe Newark wasn&#8217;t the best station to list on the sample interaction, I recalled that I didn&#8217;t know how to pronounce it either before I&#8217;d moved to the US, so I changed the sample to &#8211;

> Alexa Ask Path Tracker What time is the next train from Grove Street to World Trade Center

And submitted the skill for certification again and voila after a couple of days I got an email to let me know that my skill was now live.

The source code is available at [Github](https://github.com/nikhilbhardwaj/path-alexa-skill), feel free to share your feedback or certification experience at either place.
