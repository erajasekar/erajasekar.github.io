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

I want to publish blog from my Notion content and I found a best solution after researching many notion hosting options. In this post, I will why I decided to use notablog for my blog and how you can also publish your blog from Notion for free.

## Example Blog for Demo

[katranaithoorumarivu.com](https://katranaithoorumarivu.com/) is the blog I built using notablog and I will use it as example in this post.
It is created from this [shared notion page](https://www.notion.so/erajasekar/91b64f91c8904a36b63b3691cea91aa6?v=3c062b5462a64f6c85720b544a2b6ecd). Each [notion page](https://www.notion.so/Thirukkural-How-to-control-Anger-e26960d655a44dcc81775f824d7997aa) in table is published as a [blog post](https://katranaithoorumarivu.com/thirukkural-adhigaram-vegulamai.html). Read on to understand how this works.

## What are the requirements?

Let me describe first my requirements so that you will know if you have same needs or if this solution is right for you.
<br>

* The blog should be **SEO friendly**. For eg.
	* Should able to prettify cryptic notion urls like *`Thirukkural-How-to-control-Anger-e26960d655a44dcc81775f824d7997aa`* to more readable url *`Thirukkural-How-to-control-Anger`*
	* Should able to update html metatags so that I can customize how it appears in social media like Facebook, Twitter etc.

* Since Notion doesn't have good backup solution, I don't want blog to use same content in Notion, instead import the content to hosting site. So If lose content in my Notion, the blog won't be broken.
* Should able to use my own custom domain.
* I should to use Google Analytics for tracking.
* I am not looking for a fully automated **paid** product, but a **free low code** tool.


## Why did I decide to use notablog ? 

I popular Notion hosting tools like [Super.so](https://super.so), [HostNotion](https://hostnotion.co/), but they are all paid. The main feature they provide is prettify URL which is implemented using URL rewrite. So I found free tool [Fruition](https://fruitionsite.com/) that can do url rewrite for Notion. But the problem with Fruition and other paid solutions is that it still serves content from Notion.

Then I got an idea that I should look for static site generators that can generate blog as static html from Notion content. First, I found [notion-blog](https://github.com/ijjk/notion-blog). I liked the idea, but it didn't support all the content types. For e.g toggle list didn't work. Also, it's not easy to customize theme.

After more exploration, I found [notablog](https://github.com/dragonman225/notablog) which supports all notion formats. It has good templating system that I am able to easily customize to fit my needs.


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

## How to publish Notion blog to Github pages ?
 
The blog content is generated to `public` dir, but to use github pages we either have to use special branch `gh-pages` or special folder `docs` in master branch.
I am using `docs` folder as it is easy to copy around files. 

### Setting up GitHub Pages.

* Go to your project's settings tab.
* Scroll to GitHub pages section.
* Under source select branch as `master` and folder as `/docs`.

### Publishing blog.

Once I add/update blog content in Notion, I use the below script for publishing. You can copy this to script `publish.sh` and run it using `./publish.sh <YOUR COMMIT MESSAGE>`

<iframe id="preview-iframe" src="https://doculet.net/doc/07ef4fa571e1ae87de1d4d98af529144"
 align="middle"
 width="100%"
 height="298"
 allowfullscreen="true"
 scrolling="no"
 frameborder="0"></iframe> 

## How to setup custom domain for Notion blog ?

### Configure Github pages to use custom domain.

* Go to GitHub pages section in project's settings tab.
* Enter YOUR DOMAIN NAME under custom domain and click Save.
* This creates file name `CNAME` in `docs` dir. 
* So you should copy `CNAME` file to `public` dir using the command `cp docs/CNAME public/CNAME` to make sure CNAME file is not deleted by publish script.

### Configure Apex and CNAME records in your domain provider.

* Go to DNS Management settings of your domain provider
* Create `A` record to point your apex domain to the IP addresses for GitHub Pages. Basically add a Host record with type `A`, host `@` and value as following IP addresses.

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
* Create a `CNAME` record for host `www` to point to value `<GIT_YOUR_NAME>.github.io`. 
* Here is how I have configured it in my namecheap DNS settings.

![Namecheap DNS Settings](https://www.dropbox.com/s/myafmk86z8t3z5g/namecheap-screenshot.png?dl=0&raw=1)

* For more information refer to [this guide](https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain) from github.

## How to make Notion blog SEO friendly ?

To make a site SEO friendly, HTML meta tags like `<meta property="PROPERTY_NAME" content="VALUE">`  should be added to the `<head>` section. 

Luckily, Notablog already adds most of the required meta tags. The only tag I need to add is `og:image` to provide cover image for social sharing like facebook and twitter.

### Create custom theme in Notablog

Before adding metatags, let's look at the Notablog's directory structure and understand the theme system.

```
notablog-starter
├── config.json
├── public
├── source
│   └── notion_cache
└── themes
    └── pure
    	└── layout
    	└── assests
```

Notablog ships with one theme `pure`. This theme name is configured in `notablog-starter/config.json` to be used as default.

The `layout` directory contains the template files `index.html` , `post.html` and `tags.html` which are used to generate static html files when  `notablog generate` command is run.

I figured that to customize generated html content these template files should be updated. To easily track the changes to be made, I thought it's good idea to use my own theme. So
I created a new theme `kartranai` using steps

* Copy **pure** dir to **kartranai**. `cp -r themes/pure/ themes/kartranai`.
* Update theme value to `kartranai` in `config.json` file.
* Verify that `notablog generate .` generates content as before.


### Add SEO metatags.

Then, I added following snippet to `index.html` , `post.html` and `tag.html` files in `themes/kartranai` dir to add meta property for `og:image`.

<iframe id="preview-iframe" src="https://doculet.net/doc/42e896d52721faf1946ca9f3387f8a5d" align="middle" width="100%" height="223" allowfullscreen="true" scrolling="no" frameborder="0"></iframe>

As you can see from the code, it uses Notion Page cover image for social image, so you will need to add a page cover image to your pages for social images to show up.

### Verifying SEO metatags.

I found a handy tool [metatags.io](https://metatags.io/) to verify SEO tags. The tool will show the preview of how the site will appear in Google, facebook, twitter etc.

The below screen shot shows how the blog I created will look in Google, Twitter, Facebook.

![Katranai Thoorum Arivu Social](https://www.dropbox.com/s/6ko9z9csfv61c6v/Katranai%20Social.png?dl=0&raw=1)


## How to Add Google Analytics ?

To track a website, you will first need to create property in Google analytics to get unique tracking code. Then google analytics script has to placed in `<head>` section of all html files. Like how I customized SEO tags, I added google analytics script to `index.html` , `post.html` and `tag.html` files in `themes/kartranai`

```html
<script>
	//COPY AND INSERT CODE FROM YOUR GOOGLE ANALYTICS ADMIN SETUP.
</script>
  ```

Hope this post will help you build your own blog with Notion as CMS. You can find full source of the code in [Github](https://github.com/erajasekar/notablog-starter).





