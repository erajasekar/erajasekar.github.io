---
layout: post
title: Setting up your blog using Jekyll and hosting it on github
date: 2014-11-17
tags: jekyll blogging github
description: In this post I will provide instructions on how to setup your own blog by using my jekyll project as foundation and deploying to github pages.
---

I wrote about my journey that led to choosing [Jekyll](http://jekyllrb.com/) based [Poole](http://getpoole.com/) framework
as blogging platform for this site in my [previous post]({% post_url 2014-11-12-blogging-platform-hackers-octopress-docpad-poole %}) .
I have kept skeleton of my site in a separate `foundation` branch for others to easily use and you are free to fork mine to use for your own site.
In this post I will provide instructions on how to setup your own blog by using [my jekyll project](https://github.com/erajasekar/blog-jekyll) as foundation.
 <br>
##Setup
#####1. Clone `foundation` branch of [blog-jekyll](https://github.com/erajasekar/blog-jekyll/tree/foundation) repo.
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
$ jekyll serve --port 9999
```

Then, Open [http://localhost:9999](http://localhost:9999) in your browser to view your site.

##Customize
+ Update configurations in `_config.yml` appropriate to your site.
+ Replace `favicon.ico` , `images/profile.jpg`, `images/profile_small.jpg` in assets dir with your favicon and your profile pictures.
+ If you are using github-pages to deploy update `CNAME` file with your domain name or delete this file if you are not using custom domain.
+ Update `about.md` with your details.
+ For social sharing, register your account with [AddThis](http://www.addthis.com/) and obtain code to update  files `addthis_follow_me.html` , `addthis_follow_me_header.html` , `addthis_share.html` in `_includes` dir.
+ For disqus comments, update `disqusShortName` property in `_config.yml` and include option `comments: true` in yaml config if your posts.
+ For google analytics tracking, set up google analytics account for your site and update `_includes/google_analytics.html` with your site tracking code.
+ For showing google analytics data like page views in your site
	+ Follow [Google Analytics superProxy](https://developers.google.com/analytics/solutions/google-analytics-super-proxy) guide to publish your google analytics data on to google app engine.
	+ Then, update `googleAnalyticsSuperProxyQuery` property in `_config.yml`
+ Now you can begin writing your own posts.

##Working with Drafts

You might want to keep working in progress posts as drafts until it is ready to be published. So to create posts as drafts
simply keep them in `_drafts` dir and Jekyll will ignore them when building site. To preview your drafts locally just 
use ***--drafts*** option like `jekyll serve --port 9999 --drafts` and jekyll will show your drafts.

##Importing existing blogs to Jekyll

There are lot of tools available, if you already use other blogging platforms like wordpress or blogger and want to migrate to Jekyll.
Checkout wide range of importers available for various platforms at [import.jekyllrb.com](http://import.jekyllrb.com/).
There is also [wordpress plugin](https://github.com/benbalter/wordpress-to-jekyll-exporter/) which makes it painless to migrate from wordpress.

One common problem when migrating from existing blogs could be the permalink structure might be different in your old blog.
For eg: wordpress uses the format `~/YYYY/MM/title`, but this site uses simple format `posts/title`.
You don't want to break the links of your posts you shared everywhere TODO.

There are two possible solutions to preserve your links:

1. You can easily change permalink structure of Jekyll to [format of your choice](http://jekyllrb.com/docs/permalinks/) by tweaking `_config.yml`. 
2. If you decide to switch permalink structure of Jekyll, you can keep old links as is and setup redirects in server configuration files such as `.htaccess`
to redirect old links to correct location. <br/>
If you use github pages to deploy, you can follow [these instructions](https://help.github.com/articles/redirects-on-github-pages/)
to setup redirects in github pages easily using jekyll-redirect-from gem .

##Linking to other posts

You might often link between your posts using internal site links. You can use [post-url](http://jekyllrb.com/docs/templates/#post-url)
for this without having to worry about the URL's breaking when the site permalink style changes.
Eg: {% raw %} `{% post_url 2010-07-21-name-of-post %}` {% endraw %}


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

