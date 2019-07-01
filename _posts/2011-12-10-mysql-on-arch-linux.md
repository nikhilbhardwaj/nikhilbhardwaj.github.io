---
id: 63
title: Getting MySQL to work on arch linux
date: 2011-12-10T14:23:57-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=63
permalink: /2011/12/10/mysql-on-arch-linux/
categories:
  - arch
  - Linux
tags:
  - arch linux
  - linux
  - mysql
---
I was setting up the LAMP stack on my arch linux installation, I followed the wonderful arch wiki and had no trouble getting apache and php working but there seems to be a problem with MySQL. It installs just fine but the daemon doesn't start up.

<pre class="brush: bash; title: ; notranslate" title="">lovelock# rc.d restart mysqld
:: Stopping MySQL Server [FAIL]
:: Starting MySQL Server  [FAIL]

</pre>

I tried fixing the ownership and permissions but didn't have any success. I realized the cause of the problem after running mysqld_safe

<pre class="brush: bash; title: ; notranslate" title="">lovelock# /etc/rc.d/mysqld
usage: /etc/rc.d/mysqld {start|stop|restart}
lovelock# mysqld_safe
/usr/bin/mysqld_safe: line 531: hostname: command not found
111209 17:06:03 mysqld_safe Logging to '/var/lib/mysql/.err'.
/usr/bin/mysqld_safe: line 608: hostname: command not found
111209 17:06:03 mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql
111209 17:06:03 mysqld_safe mysqld from pid file /var/lib/mysql/.pid ended
</pre>

I installed hostname

<pre class="brush: bash; title: ; notranslate" title="">pacman -S inetutils

</pre>

But that didn't solve it either and I had to do this to fix it

<pre class="brush: bash; title: ; notranslate" title="">rm -rf /var/lib/mysql/*
mysql_install_db --user=mysql --basedir=/usr
</pre>

This removes the databases and creates a new copy. For me it wasn't an issue as this is a fresh install but you should be careful when upgrading mysql. Its always handy to back up the databases first.
