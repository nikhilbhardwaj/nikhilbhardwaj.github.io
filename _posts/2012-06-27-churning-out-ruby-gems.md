---
id: 119
title: Churning out ruby gems
date: 2012-06-27T00:14:40-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=119
permalink: /2012/06/27/churning-out-ruby-gems/
categories:
  - Programming
  - tech tips
---
If you didn't already know then let me tell you that I'm a huge fan of the <a href="http://www.ruby-lang.org" target="_blank">ruby programming language</a>. I have dabbed with a few imperative languages and none can come close to ruby, it's syntax is like sugar and libraries like alcohol. You get addicted to them once you start. I use gems (that's the fancy name for ruby libraries) from time to time. They can be used in both programs that you write and some also provide a standalone binary. But that is hardly the fascinating part, what is fascinating is that how easy it is to create them. I just created one and will mention the steps briefly so that you are also inspired to try your hand at it.<!--more-->To create the initial directory structure and to initialize an empty git repository for our beloved gem we need just one command.

<pre class="brush: plain; title: ; notranslate" title="">bundle gem NittResults</pre>

It goes without saying that you can replace <a title="The Source code for the NittResults gem" href="https://github.com/nikhilbhardwaj/NittResults" target="_blank">NittResults</a> with the name that you want to give your gem. Next you can add a remote origin if you wish to publish the gem on github or another source code control portal.

Next you need to add the code to the .rb file in the lib directory. Make changes to the gemspec if your gem has other dependencies and also to write a short description.
Now you can build the gem with

<pre class="brush: plain; title: ; notranslate" title="">bundle exec rake install </pre>

and then publish it with

<pre class="brush: plain; title: ; notranslate" title="">rake publish </pre>

And that's all that needs to be done.

I'll briefly describe what <a title="Getting graphics.h to work on Windows and Linux" href="https://rubygems.org/gems/NittResults" target="_blank">my gem</a> does, it fetches the results of me and my classmates from our university website and stores everyone's result in text files. This way I can go over them all at once without having to navigate through the clunky website that the university has. This gem is minimal and I have a few improvements planned, if this generates some interest then I'll think about implementing them. I'll surely be writing more gems in the due course of time let me know if you have written one after reading this.
