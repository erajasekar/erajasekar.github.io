---
layout: post
title: Creating awesome blogs with static site generators
date: 2014-11-05
tags: jekyll blogging github docpad octopress
description: In this post I will walk through my discovery of finding right blogging platform for my site, my experiences with static site generators and things I learned.
---

In this post I will walk through my discovery of finding right blogging platform for my site, share my experiennces, findings and learnings along the way.
 
When I decided to blog, I researched on next generation blogging platforms for hackers. 
Mainstream blogging platforms like wordpress, blogger, tumblr are designed for naive users and aren't best for developers. 
Because those platforms doesn't support features programmers would want like code syntax highlighting, theming using css frameworks, 
markdown language support, integration with source code repositories etc. <!-- TODO bulletize -->

###Static site generators:
I learned that many static site generators are used for blogging platform. The static site generators are basically template engines 
that takes templated dynamic content and runs it through various processors and converters to generate static html pages. 
***The idea that dynamic content doesn't need to be always served by a backend server, rather a template engine could pre generate 
static site from dynamic content is brilliant***. Using static site generators provided these benefits and features which I was hunting for

+ Syntax highlighting for code snippets.
+ Customizable layouts and themes using frontend frameworks like Bootstrap
+ Write content using Markdown language.
+ Manage code in source control.
+ Easy deployment and hosting on github pages or other hosting providers like [Heroku](https://www.heroku.com/).
+ Easy integration with social sharing like facebook, twitter and disqus comments.
+ Mobile friendly response UI.
 
After bit of research narrowed down my choices to [Octopress](http://octopress.org/) based on and [Docpad](https://docpad.org/) and played around with both.

###Impressions with Octopress

[Octopress](http://octopress.org/) (advertised as is *A blogging framework for hackers.*) is blogging framework on top of [Jekyll](http://jekyllrb.com/) static site generator. 
Of course, Jekyll itself could be used, but Octopress makes it easier by providing ruby scripts and themes out of the box. 
Basically it encompasses Jekyll ,Jekyll plugins, Rake tasks and Themes. The setup process is very easy - just clone the [octopress repo](https://github.com/imathis/octopress),
tweak basic configs and start creating posts as Markdown files. I was able to get a blog running in just few minutes, 
but I wasn't satisfied with it for couple of reasons

+ I wasn't pleased with default theme. I had to manually customize the CSS instead of using popular frontend frameworks 
like [Bootstrap](http://getbootstrap.com/), [Html5Boilerplate](http://html5boilerplate.com/)
+ I didn't like the fact that I need to check in the octopress code itself (scripts, plugins etc.) along with my posts into source control. This will make upgrading to new version of octopress convoluted.

I didn't spend too much time on octopress, as I found some people <sup><a href="#1.-people-migrating-from-octopress-to-docpad">1</a></sup> moved from octopress to docpad.

###Experiences with Docpad

[Docpad](https://docpad.org/) is highly customizable and extensible site generation platform built with Node.js. It can be used to build any kind of Content Mangement System (CMS), not just blogs. It supports several languages like haml, jade, coffeekup including markdown and has myraid of [plugins](https://docpad.org/docs/plugins) for everything you need for a blog.
It also comes with many prebuilt [skeletons](https://docpad.org/docs/skeletons) for theming.


###Moving over to Jekyll using Poole Laynon theme

######1. People migrating from Octopress to Docpad

[SriptyBooks.com](http://blog.scriptybooks.com/from-jekyll-octopress-to-docpad/)<br/>
[maximilianschmitt.me](http://maximilianschmitt.me/posts/from-wordpress-to-octopress-to-docpad/)<br/>
[ewal.net](http://www.ewal.net/2013/10/08/blogging-with-docpad/)

