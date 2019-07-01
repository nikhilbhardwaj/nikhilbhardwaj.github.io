---
id: 50
title: Getting graphics.h to work on Windows and Linux
date: 2011-08-01T20:24:34-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=50
permalink: /2011/08/01/graphics-h-windows-linux/
categories:
  - Linux
  - Programming
  - Sabayon
tags:
  - bgi
  - graphics.h
  - windows
---
We have an introductory Computer Graphics course at our university this semester, we will be working with BGI(Borland Graphics Interface) which has its origins in Borland Turbo C. It goes without saying that I'm not a big fan of Turbo C, its a wonder why its so popular in India even though its so out of date. I have [mingw](http://www.mingw.org) set up on windows and also dual boot sabayon linux. I'll set it up on both and list the steps here. This should work with Bloodshed Dev-Cpp but your mileage might vary.<!--more-->

Let us set it up for windows first, you need to download the two files [graphics.h](http://nikhilbhardwaj.in/resources/graphics/graphics.h) and [libbgi.a](http://nikhilbhardwaj.in/resources/graphics/libbgi.a). Copy graphics.h to your includes directory ( C:\MinGW\include in my case ) and the libbgi.a to the lib directory ( C:\MinGW\lib ). The only other thing that needs to be done is to compile your programs with the following linker options

<pre class="brush: plain; title: ; notranslate" title="">-lbgi
-lgdi32
-lcomdlg32
-luuid
-loleaut32
-lole32
</pre>

Here's a sample program that you can use to check your setup.

<pre class="brush: plain; title: ; notranslate" title="">#include &lt;iostream&gt;
#include &lt;graphics.h&gt;

using namespace std;

int main(int argc,char** argv)
{
	int gd=DETECT,gm;
	initgraph(&gd,&gm,0);
	rectangle(50,50,500,200);
	getch();
	closegraph();
	return 0;
}
</pre>

This can be compiled in a this manner.

<pre class="brush: plain; title: ; notranslate" title="">C:\Users\nikhil\Documents\graphics_h_setup&gt;g++ rectangle.cpp -o
rectangle -lbgi -lgdi32 -lcomdlg32 -luuid -loleaut32 -lole32
</pre>

The Output should be similar to the following.
![](/assets/uploads/2011/08/rectangle_screenshot.png)

After this you should be able to try your own programs at your leisure. Now we move onto the instructions for setting the same up on linux. Its much easier for us to install this in linux, the detailed steps are as follows. We'll build from source we need to grab [libgraph](http://savannah.nongnu.org/projects/libgraph). Now its a simple configure make install cycle. You can use the following commands to accomplish the entire thing.

<pre class="brush: plain; title: ; notranslate" title="">[nikhil@lovelock ~]$ mkdir Sources && cd Sources
[nikhil@lovelock ~]$ wget http://ftp.twaren.net/Unix/NonGNU/libgraph/libgraph-1.0.2.tar.gz
[nikhil@lovelock ~]$ tar xf libgraph-1.0.2.tar.gz
[nikhil@lovelock ~]$ cd libgraph-1.0.2
[nikhil@lovelock ~]$ ./configure --prefix=/usr/lib
[nikhil@lovelock ~]$ make -j2
[nikhil@lovelock ~]$ sudo make install
[nikhil@lovelock ~]$ make clean && cd ~
</pre>

The same sample program can be run in the following manner

<pre class="brush: plain; title: ; notranslate" title="">[nikhil@lovelock graphics-progs]$ g++ rectangle.cpp -o rectangle -lgraph
[nikhil@lovelock graphics-progs]$ ./rectangle
</pre>

That's all there is to it, you're on your way. I'm not convinced that this is the best way either, one should probably learn something like OpenGL instead. Having said that this is better than Turbo C any day. Drop in a line if you have any questions or clarifications with this.
