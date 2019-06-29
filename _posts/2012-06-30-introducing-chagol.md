---
id: 127
title: Introducing Chagol!
date: 2012-06-30T16:10:31-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=127
permalink: /2012/06/30/introducing-chagol/
categories:
  - Programming
---
Having learnt how easy it was to develop ruby gems, I thought of putting my newly learned skills to the test and the result is <a title="The magnificent chagol" href="https://rubygems.org/gems/chagol" target="_blank">chagol</a>. Any work of software starts by scratching a developer&#8217;s personal itch and chagol does that for me. Before I tell you how to get hold of chagol, let me tell you why I&#8217;ve started developing it. As a student most of my communication is through text messages and quite often when I&#8217;m working on something I get a message that I have to respond to. I typically reply back using the phone or use a service like way2sms to do the same both of these take more time than that ought be taken. I&#8217;m a command line junkie so a command line tool with a simple interface would be ideal for me and since none existed I thought I&#8217;d write one myself.<!--more-->The goals that I had in mind before starting out were to adhere to the unix philosophy and hence chagol does one task only and I&#8217;d like to think it does that very well. The interface had to be simple to use and intuitive, no one likes command like tools that make you learn a tonne of syntax, this initially sounded hard to me but ruby&#8217;s OptionParser made this almost trivial. If you wish to use chagol, you should look at the readme in the

<a title="Chagol is developed with git" href="https://github.com/nikhilbhardwaj/chagol" target="_blank">github repository</a>. The only prerequisites are having a flavor of ruby > 1.9 on your machine along with an account with way2sms or 160by2.

I&#8217;ll briefly write about configuring it after installation, there is one file that is mandatory, it should contain your way2sms/160by2 username i.e. your mobile no. and the password for the same. To edit it, you need to run

<pre class="brush: plain; title: ; notranslate" title="">vim ~/.chagol/config.rb </pre>

vim can be replaced with the editor of your choice. After this is done you should be able to send messages with it, the usage is

<pre class="brush: plain; title: ; notranslate" title="">chagol -t 9876543210 -m "Your message" </pre>

but remembering numbers is something that I find nearly impossible and so we need contacts too so that you could send messages like

<pre class="brush: plain; title: ; notranslate" title="">chagol -t Nikhil,Pinnu -m "Chagol rocks!" </pre>

yes you guessed it, you can send messages to multiple people at the same time too but you need to specify your contacts once before chagol can use them, to do this you need to edit this file

<pre class="brush: plain; title: ; notranslate" title="">vim ~/.chagol/contacts.json </pre>

Add as many contacts as you want to, you can use the one dummy contact that you&#8217;ll find there to use as a template for the others, please keep the id&#8217;s unique. I&#8217;m thinking of implementing lists using those if enough people using chagol ask for it.

Another thing that you need to know is that chagol isn&#8217;t only a command line tool, it can easily be used with any existing ruby project (See the <a title="Chagol is developed with git" href="https://github.com/nikhilbhardwaj/chagol" target="_blank">Readme on github</a> if you want to use it from your website to send messages) to send messages to mobile phones in India also it can&#8217;t send international messages either.

Perhaps another feature can be the ability to easily add contacts, since I&#8217;m the one implementing chagol that can be done too, do leave a comment if you used chagol to let me know how you found it and also if there are some features that you&#8217;d like implemented or bugs that need fixed.

&nbsp;

P.S : The story behind the name is best left untold for now 😉
