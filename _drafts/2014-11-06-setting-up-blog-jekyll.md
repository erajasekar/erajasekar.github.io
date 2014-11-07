---
layout: post
title: Setting up your blog using Jekyll
tags: jekyll blogging
description: In this post I will provide instructions on how to setup your own blog by using jekyll project as foundation.

---

This blog is built with [Jekyll](http://jekyllrb.com/) and you can fork mine to use it on your own site if you would like. In this post I will provide instructions on how to settup your own blog by using mine as foundation.
 
##Setup
#####1. Clone foundation branch [blog-jekyll](https://github.com/erajasekar/blog-jekyll/tree/foundation) of repo.
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

Then, Open [http://localhost:9999](http://localhost:9999) in your browser.

##Customize
+ Update configurations in `_config.yml` appropriate to your site.
+ Replace `favicon.ico` , `images/profile.jpg`, `images/profile_small.jpg` in assets dir with yours.
+ If you are using github-pages to deploy update `CNAME` file with your domain name or delete this file if you are not using custom domain.
+ Update `about.md` with your details.
+ For social sharing, register your account with [AddThis](http://www.addthis.com/) and obtain code to update  files `addthis_follow_me.html` , `addthis_follow_me_header.html` , `addthis_share.html` in `_includes` dir.
+ For disqus comments, update `disqusShortName` property in `_config.yml`.
+ For google analytics tracking, update `_includes/google_analytics.html` with your site tracking code.
+ For showing google page views in your site
	+ Follow [Google Analytics superProxy](https://developers.google.com/analytics/solutions/google-analytics-super-proxy) guide to publish your google analytics data on google app engine.
	+ Then, update `googleAnalyticsSuperProxyQuery` property in `_config.yml`
+ Now you can add your own posts.

##Deployment
+ To deploy to github pages, create a repository `youruserame.github.io` and push your code to master branch.
+ For other deployment options, refer to [Jekyll documentation](http://jekyllrb.com/docs/deployment-methods/).

##Custom domain
If you would to setup your own custom domain for your blog,

+ Create a CNAME file containing your custom domain at the root of your git repository
+ In your DNS provider configuration, create a CNAME record that points from that domain to `yourusername.github.io`
+ In your DNS provider configuration, create A records that resolve to the following IP addresses
	+ 192.30.252.153
	+ 192.30.252.154
+ Here is snapshot of how I configured my domain [erajasekar.com](http://erajasekar.com) with DNS provider [namecheap.com](http://namecheap.com)

<img  src="{{ site.baseurl }}assets/images/namecheap-dns-settings.png" alt="erajasekar.com dns settings in namecheap.com" />

