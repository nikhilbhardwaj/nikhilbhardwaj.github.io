---
id: 147
title: Fixing the keyboard on a hackintosh
date: 2012-08-14T22:07:05-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=147
permalink: /2012/08/14/fix-hackintosh-keyboard/
categories:
  - mac
  - tech tips
tags:
  - hackintosh
  - iatkos
  - tilde
---
I installed iAtkos L2 on my Acer 5742G laptop and it works really well, there was one thing that has been bugging me. I couldn't press ~ on the keyboard and using the terminal was painful when it came to specifying paths relative to my home directory.

After some looking around I found this application <a href="https://github.com/tekezo/KeyRemap4MacBook" target="_blank">KeyRemap4MacBook</a>. As the name suggests it allows us to remap keys on the keyboard and assign them different functions. The problem I had was that I got <a href="http://en.wikipedia.org/wiki/Section_sign" target="_blank">§</a>** **instead of the usual backquote(\`). Here's the relevant xml snippet that performs the desired conversion

<pre class="brush: plain; title: ; notranslate" title="">&lt;?xml version="1.0"?&gt;
&lt;root&gt;
&lt;item&gt;
&lt;name&gt;Fix Tilde&lt;/name&gt;
&lt;identifier&gt;private.fix_tilde&lt;/identifier&gt;
&lt;autogen&gt;--KeyToKey-- KeyCode::UK_SECTION, KeyCode::BACKQUOTE&lt;/autogen&gt;
&lt;/item&gt;
&lt;/root&gt;

</pre>

&nbsp;

The best part about this is that it's an open source project. I didn't know about the keycodes and had problem finding the ones that I needed, so I asked by opening an <a href="https://github.com/tekezo/KeyRemap4MacBook/issues/82" target="_blank">issue on github </a>and the author took the time out to help me. I absolutely love the open source community. Hopefully this will help someone else who had a similar issue. This application can also be useful for those who have keyboards with multimedia keys that don't work out of the box for hackintoshes.
