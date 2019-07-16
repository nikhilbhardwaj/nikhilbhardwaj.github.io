---
id: 1002
title: 'Dr. Jekyll and Mr. AWS'
date: 2019-07-16T13:42:47-04:00
author: nikhil
layout: post
permalink: /2019/07/16/dr-jekyll-and-mr-aws/
categories:
  - aws
  - blogging
  - git
---
For many years, I've hosted my blog with Wordpress on a hosting provider called VlexoFree. Earlier in the year Eli, the proprietor of [VlexoFree announced](https://web.archive.org/web/20190419184558/http://www.vlexofree.com/announcement.html) that they were shutting down. I did thank Eli personally over email and want to do so again publically for the great service that he provided. Thank you Eli and I wish you the very best in whatever endeavors you may have lined up in the future. Vlexofree provided a typical CPanel based offering with a generous free tier. When I first started using it I was a student, I vividly remember buying my first domain name, setting up my mailserver and website, those were the days...

Fast forward to the announcement, I needed to come up with a way to host my blog elsewhere. One option definitely was to setup another Wordpress instance elsewhere but before doing that I reviewed my blogging behavior
- I blog infrequently, sometimes in bursts(a few posts in months) and then a hiatus(sometimes even 6 months)
- Comments on posts or lack thereof (Since I don't write frequently I don't have a dedicated base or comments on articles, I do get occasional emails from readers which I love)

Based on these I felt that Wordpress was overkill for my usecase, it required frequent version upgrades and I wasn't really looking forward to set up another stack. Over the last couple of years I've become familiar with markdown, I'm too lazy to learn Tex but I do like how omnipresent markdown is. We use it internally at work to communicate on issues and tickets and I love how it's so lightweight and yet brings text to life. With comments out of the equation a static site generator that supported markdown was perfect for me, I already knew about Github pages and jekyll, so I decided to give it a shot and to convert my blog from Wordpress to jekyll. There's a Wordpress plugin that converts all posts into markdown and sets up a jekyll project. I had to do some work to fix the links to images and other assets, that along with finding a theme was all it took to get it up and running on Github pages.

Without a doubt, Github pages is the best and most straightforward way of hosting a jekyll site. The only downside is that they only allow one for each (free) account. I did some searching to see what other alternate options were available and it turns out there are quite a few, namely
- Heroku
- netlify
- DigitalOcean
- aws
- and many others

I don't want to be blowing AWS's trumpet but of late I've been moving more and more of my projects into AWS. I like the fact that it's cost effective, secure and really easy to manage. So I'll talk briefly about setting up my second Jekyll website on AWS. This isn't an authoritative guide or listing, far from it. I do feel that it is the easiest and most convenient way though.

AWS has a really cool service called Amplify, in reality Amplify is a lot more that a hosting service with it's own build tools and a set of libraries for the popular Javascript frameworks. For my usecase I don't particulary care about yet another common Javascript library that Amplify is trying to be, what I do really like is the ability to hook up a Git repository. Then to run one of many build systems to generate the website and to finally deploy it (and scale it if needed). It also has support for SSL certificates and custom domains (though the documentation is lacking; this is a common theme for most of the AWS services).

There was only one complication that I encountered and that was with attempting to setup a Github repository to back my site. This is ofcourse supported but the amount of permissions that Amplify wants to support this is disgusting, they want access to all your public and private repositories along with all repositories of organizations that you're a part of unless the organziation has explicitly restriced access to their repositories. This being unacceptable to me I decided to then use AWS Code Commit to host the repository to mirror the main Github repository.

Git is an awesome tool and it's easy enough to setup multiple remotes. [This Gist](https://gist.github.com/rvl/c3f156e117e22a25f242) was particulary helpful. With the repository hook setup, Amplify had no problem building my site and eploying it. They also setup a SSL certificate for my custom domain, getting the actual redirection setup was a bit tricky AWS recommends that you move your domain to Route53 but I was having none of that. I manage all my domains with Cloudflare and instead of an ANAME or Alias record a CNAME record worked just fine. Cloudflare supports DNS flattening which makes it possible to route the domain elsewhere and not break mail etc that may be configured already. Thank you Cloudflare, you are awesome.

Lastly as I summarize, it's very important to understand the pricing structure. Given my writing pattern I'll only have a few builds a month, the storage size is also paltry as is the overall bandwidth so it should only cost me a few cents if that to host. Other serices like Heroku and Netlify may have a better pricing model and are worth considering as well.
