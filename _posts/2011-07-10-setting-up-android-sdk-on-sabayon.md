---
id: 33
title: Setting Up Android SDK on Sabayon
date: 2011-07-10T02:12:54-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=33
permalink: /2011/07/10/setting-up-android-sdk-on-sabayon/
categories:
  - android
  - Linux
  - Sabayon
tags:
  - android sdk
  - linux
  - setup guide
---
Mobile application development seems to be in vogue these days, with the iPhone and Android platforms being the top contenders. iPhone had all of the market to itself sometime back  but now android is making progress at a very fast rate. I've decided to get my feet wet and get to know the basics of developing for android. The android sdk can be installed on windows, linux as well as mac osx. The installation instructions on the android developer are perfect for windows, mac and ubuntu (and its derivatives). Its not plain sailing for others, a few hacks are required here and there but it all works eventually. These instructions are tested on sabayon 6 kde x86_64 but should work with other editions too.<!--more-->

First we need to install the basic packages these are apache-ant which is a build tool for java, the android sdk update manager and eclipse. We need jdk too but I have openjdk installed out of the box so I wont bother with it, if we run into trouble with this then we can always switch jdk's. All the required packages can be installed with one single command, but be warned that it will download quite a volume so be sure to have a fast internet connection.
Run the following command as root or use sudo if you prefer:

<pre class="brush: bash; title: ; notranslate" title="">lovelock ~ # su -
lovelock ~ # equo install ant dev-util/android-sdk-update-manager eclipse-sdk

</pre>

Now wait a while for it to complete, after it is done then we need to fix our path to include the location where android sdk update manager is installed, sabayon installs it in /opt. Add these lines to your .bash_profile

<pre class="brush: bash; title: ; notranslate" title=""># Fixups for android
export PATH=$PATH:/opt/android-sdk-update-manager/tools:
export ANDROID_SWT=/usr/share/swt-3.5/lib

</pre>

Now source the file to update the path without the need to logout and then back in and then run android.

<pre class="brush: bash; title: ; notranslate" title="">nikhil@lovelock ~ $ source ~/.bash_profile
nikhil@lovelock ~ $ android

</pre>

If you can't find android in the path then you haven't updated it correctly review the previous step carefully and then proceed.
Now you can choose the packages that you want downloaded, typically you'll need any one platform depending on what device you have, otherwise I'd recommend installing the latest version for phones as of now its 2.3.3. Click install, again this will take some time downloading, after this you can create your emulator too.

All this was smooth sailing but getting things to work with eclipse seems to have its hiccups here's what we need to do in order to get integrate android and eclipse. If we try to add the ADT Plugin for Eclipse following the standard instructions then the following error results:

<pre class="brush: plain; title: ; notranslate" title="">Gef missing
Cannot complete the install because one or more required items could not be found.
  Software being installed: Android Development Tools 12.0.0.v201106281929-138431 (com.android.ide.eclipse.adt.feature.group 12.0.0.v201106281929-138431)
  Missing requirement: Android Development Tools 12.0.0.v201106281929-138431 (com.android.ide.eclipse.adt.feature.group 12.0.0.v201106281929-138431) requires 'org.eclipse.gef 0.0.0' but it could not be found.

</pre>

This can be solved by either downloading eclipse from its site and not the package manager or with the following fix, Open up eclipse and then:

<pre class="brush: plain; title: ; notranslate" title="">In Help-&gt;Install New Software -&gt;Add
add new 3 sites, as below:

    name: Galileo
    link: http://download.eclipse.org/releases/galileo/

    name: Gef
    link: http://download.eclipse.org/tools/gef/updates/releases/

    name: Android
    link: https://dl-ssl.google.com/android/eclipse/
</pre>

After this we need to install the missing dependencies, this can be done by following the steps below:

<pre class="brush: plain; title: ; notranslate" title="">In Help-&gt;Install New Software-&gt; Work with

    'Galileo'-&gt;"Web, XML and java EE Devlopment"-&gt;"WST Server Adapter"
    and install.
</pre>

You'll be prompted to restart eclipse, do so and then:

<pre class="brush: plain; title: ; notranslate" title="">This time, in Help-&gt;Install New Software-&gt; Work with

    Gef:
    choose the "Gef"-&gt; "[latest version]" and install.
</pre>

Now restart eclipse and for the last time:

<pre class="brush: plain; title: ; notranslate" title="">In Help-&gt;Install New Software-&gt; Work with

    Android:
    choose the "Android"-&gt;"Android Development Tools" and install.
</pre>

After another restart of eclipse you're almost all set. The last thing that needs to be done is to set the Android sdk path to /opt/android-sdk-update-manager in Window->  Preferences-> Android.

If you've managed to get here then easy part is done, android sdk is installed and eclipse is configured to run it. Now begins the journey of learning android. I'll document it along the way, Hopefully this helps other sabayon users to install the android sdk without any pains.
