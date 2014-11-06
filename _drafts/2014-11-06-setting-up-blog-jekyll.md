---
layout: post
title: Setting up your blog using Jekyll.
tags: jekyll blogging
date: 2014-11-06
comments: false
---
This is source code of my blog at [erajasekar.com blog](http://erajasekar.com) hosted using [github pages](https://pages.github.com/). It's build using [Jekyll](http://jekyllrb.com/) uses [Lanyon](http://lanyon.getpoole.com/) theme.

I actually forked this from [anandmanisankar.com](http://anandmanisankar.com/) as he had all the social plugins configured like the way I wanted.

You can also fork mine and use it for your own site if you would like by following these steps.

##Setup
#####1. Clone [foundation branch](https://github.com/erajasekar/blog-jekyll/tree/foundation) of this repo.
* Install [Jekyll](http://jekyllrb.com/)  
```bash
$ gem install jekyll
```

#####2. If you are deploying to github, Install github-pages gem  
```bash
$ gem install github-pages
```

#####3. If you plan to customize css files, Install Grunt for compiling css to single minified file  
```bash
$ sudo npm install -g grunt-cli
$ npm install grunt --save-dev
```
  Then, when you edit css files, run `grunt` to recompile css.

##Running 

To get your site running locally, start Jekyll server
```bash
$ jekyll server --port 9999
```

Open [http://localhost:9999](http://localhost:9999) in your browser.

##Customize
+ Update configurations in `_config.yml` appropriate to your site.
+ Replace `favicon.ico` , `images/profile.jpg`, `images/profile_small.jpg` in assets dir with yours.
+ If you are using github-pages to deploy updtate `CNAME` file with your domain name.
+ Update `about.md` with your details.
+ For social sharing, register your account with [AddThis](http://www.addthis.com/) and obtain code to update following files
	{% highlight bash%} . | |-- _includes | | | |-- addthis_follow_me.html | |-- addthis_follow_me_header.html | |-- addthis_share.html
	{% endhighlight %}
 
+ For disqus comments, update `disqusShortName` property in `_config.yml`.
+ For google analytics tracking, update `_includes/google_analytics.html` with your site tracking code.
+ For showing google page views in your site
	+ Follow [Google Analytics superProxy](https://developers.google.com/analytics/solutions/google-analytics-super-proxy) guide to publish your google analytics data on google app engine.
	+ Then update `googleAnalyticsSuperProxyQuery` property in `_config.yml`
  
+ Start adding your own posts.