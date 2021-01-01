---
layout: post
title: How to publish SEO friendly blog from Notion for Free?
date: 2020-12-31
draft: false
tags: productivity notionhq notion blog
comments: true
description: TODO
analytics: true
---

I want to publish blog from my Notion content and I researched notion hosting solutions that are available. In this post, I will why I decided to use notablog for my blog and how you can also publish your blog from Notion for free.

## What are my requirements?

Let me describe my requirements so that you will know if you have same needs or if this solution is right for you.
<br>

* The blog should be SEO friendly. For eg.
	* should able to prettify default notion urls like `Notion-Icons-App-8bf15be950c54b3ebbed3636324fc22` to `Notion-Icons-App`
	* should able to update html metatags how it appears in social media like facebook, twitter etc.

* Since Notion doesn't have good backup solution, I don't want blog to use same content in Notion, instead import the content to hosting site. 
* Should able to use custom domain.
* I am not looking for a fully automated paid product, but a free low code tool.

## Why did I decide to use notablog ? 

There are some of the popular Notion hosting tools like [Super](https://super.so), [HostNotion](https://hostnotion.co/), but they are paid. The main feature they provide is pretty URL which is implemented using URL rewrite. So I found free tool [Fruition](https://fruitionsite.com/) that can do url rewrite for Notion. But the problem is that it still serves content from Notion.

So I searched for static site generators that can create blog from Notion content and I found [notion-blog](https://github.com/ijjk/notion-blog). I liked the idea, but it didn't support all the content types. For e.g toggle list didn't work. Also, it was not easy to customize theme.

Finally, I found [notablog](https://github.com/dragonman225/notablog) which supports all notion formats. It has good templating system that is very easy to customize.


## How to create blog from Notion ?

The step's on the project's [README](https://github.com/dragonman225/notablog) worked great. I have included it here for easy reference.

1. Install Notablog.
   ```bash
   npm i -g notablog
   ```

2. Clone the [`notablog-starter`](https://github.com/dragonman225/notablog-starter) repository.
   ```bash
   git clone https://github.com/dragonman225/notablog-starter.git
   ```
   
3. Duplicate this [Notion table template](https://www.notion.so/b6fcf809ca5047b89f423948dce013a0?v=03ddc4d6130a47f8b68e74c9d0061de2).

4. Make the table you've duplicated **public** and **copy its URL** for the next step.

5. Go into `notablog-starter/` directory, open `config.json`. Replace the value of `url` with the URL of the table you've duplicated.

6. Inside `notablog-starter/` directory, run command:

   ```bash
   notablog generate .
   ```

7. After it finishes, go to `notablog-starter/public/` directory, open `index.html` with a browser to preview your site.


## How to make blog SEO friendly ?

todo 
* Adding analytics.

## How to deploy blog to Github pages ?
 
todo



