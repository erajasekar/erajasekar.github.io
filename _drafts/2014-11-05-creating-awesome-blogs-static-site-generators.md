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

I didn't spend too much time on octopress, as I found octopress is not flexible and some people <sup><a href="#1.-people-migrating-from-octopress-to-docpad">1</a></sup> moved from octopress to docpad.

###Experiences with Docpad

[Docpad](https://docpad.org/) is highly customizable and extensible site generation platform built with Node.js. It can be used to build any kind of Content Mangement System (CMS), not just blogs. It supports several languages like haml, jade, coffeekup including markdown and has myraid of [plugins](https://docpad.org/docs/plugins) for everything you need for a blog.
It also comes with many prebuilt [skeletons](https://docpad.org/docs/skeletons) for theming.

The plain vanilla docpad doesn't provide features I needed for blog like generating menus, labeling with tags, listing archieves and requires lot of customization using various plugins. Luckily I found [ytechie.com](http://www.ytechie.com/) that had all the features I needed so I cloned his github [repo](https://github.com/ytechie/ytechie-docpad) to create my own site. I did not had prior experience in [Node.js](http://nodejs.org/), so I had to instantly learn lot of modules in node ecosystem like [coffee script](http://coffeescript.org/), [eco templates](https://github.com/sstephenson/eco) and it was good oppurtunity for me to familarize myself with Node.js. After some struggle I finally managed to get my blog up and running. Then, I used [docpad-ghpages ](https://github.com/docpad/docpad-plugin-ghpages) plugin to host it on github. 

Meanwhile, in my work at [salesforce.com](http://www.salesforce.com/), We were looking for better way to document our application operational and troubleshooting guides. We have been using google sites, but it doesn't support syntax highlighting or reusing snippets or create any dynamic content. Also using Rich text editor is not as productive as Markdown. We also wanted better process around reviewing documentation and tracking changes. Docpad turned out to be ideal choice. I did quick proof of concept for a hackday event and it received huge acclamation from colleagues.


###Migrating Poole using Laynon theme

Short time ago, I came across [anandmanisankar.com](http://anandmanisankar.com/) and immediately liked look and feel of the site. I learnt that it also built using Jekyll, but based on [Poole](http://getpoole.com/) framework. Poole provides basic scaffolding for blog and beautiful themes [hyde](http://hyde.getpoole.com/) and [laynon](http://lanyon.getpoole.com/). I was able to get it running in just few minutes. I was able to quickly preview articles I created with docpad as I need to simply copy markdown files to `_posts` directory. I decided to migrate my blog over to Poole laynon theme because of following benefits.

+ Unlike octopress, I don't have to customize the theme or checkin ruby code into source control. The laynon theme is perfect for me and it had minimal css and layout template files to checkin to source control.
+ It is not so much complex as docpad, so it will be easy to maintain.
+ It provides blogging features out of the box and I don't have to customize much.
+ Github [natively supports Jekyll](https://help.github.com/articles/using-jekyll-with-pages/) so I can directly publish this Jekyll project to github without having to pre-generate static html files. 

Fortunately, [anandmanisankar.com](http://anandmanisankar.com/) had all the custom features I needed like social sharing with facebook, twitter, disqus comments and google analytics tracking. It also displays google analytics data like page views in posts which is pretty cool. So I cloned anandmanisankar's [git repo](https://github.com/msanand/msanand.github.io) to create my own blog and migrated over my posts from Docpad. The migration was pretty smooth and did not take very long. While doing this I kept basic skeleton in a separate branch so that others can easily clone and use it for their site. I my next post I will provide instructions on how to setup your own site based on my project as foundation.


###Conclusion

Octopress would be best option if you want to  get started quickly and use it as it without much customization. Docpad is very flexible and extensible to create any kind of site. But it is more complex and has steep learning curve if you are not familiar with Node.js. Poole provides basic scaffolding, beautiful themes and right amount of freedom for customization. I feel poole is the right choice for my requirements.

######1. People migrating from Octopress to Docpad

[SriptyBooks.com](http://blog.scriptybooks.com/from-jekyll-octopress-to-docpad/)<br/>
[maximilianschmitt.me](http://maximilianschmitt.me/posts/from-wordpress-to-octopress-to-docpad/)<br/>
[ewal.net](http://www.ewal.net/2013/10/08/blogging-with-docpad/)

