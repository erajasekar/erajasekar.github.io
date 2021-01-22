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

## Example Blog

I will use [this blog](https://katranaithoorumarivu.com/) that I built using notablog as example in this post. It is created from this [shared notion page](https://www.notion.so/erajasekar/91b64f91c8904a36b63b3691cea91aa6?v=3c062b5462a64f6c85720b544a2b6ecd). Each [page in notion table](https://www.notion.so/Thirukkural-How-to-control-Anger-e26960d655a44dcc81775f824d7997aa) is published as a [blog post](https://katranaithoorumarivu.com/thirukkural-adhigaram-vegulamai.html). 

## What are my requirements?

Let me describe my requirements so that you will know if you have same needs or if this solution is right for you.
<br>

* The blog should be SEO friendly. For eg.
	* should able to prettify default notion urls like `Notion-Icons-App-8bf15be950c54b3ebbed3636324fc22` to `Notion-Icons-App`
	* should able to update html metatags so that I can customize how it appears in social media like facebook, twitter etc.

* Since Notion doesn't have good backup solution, I don't want blog to use same content in Notion, instead import the content to hosting site. 
* Should able to use custom domain.
* I should to use Google Analytics for tracking.
* I am not looking for a fully automated paid product, but a free low code tool.


## Why did I decide to use notablog ? 

There are some of the popular Notion hosting tools like [Super](https://super.so), [HostNotion](https://hostnotion.co/), but they are paid. The main feature they provide is prettify URL which is implemented using URL rewrite. So I found free tool [Fruition](https://fruitionsite.com/) that can do url rewrite for Notion. But the problem is that it still serves content from Notion.

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

## How to deploy blog to Github pages ?
 
The blog content is generated to `public` dir, but to use github pages we either have to use special branch `gh-pages` or special folder `docs` in master branch.
I am using `docs` folder as it is easy to copy around files. 

### Setting up GitHub Pages.

* Go to your project's settings tab.
* Scroll to GitHub pages section.
* Under source select branch as `master` and folder as `/docs`.

### Publishing blog.

Once I add/update blog content in Notion, I use the below script for publishing. You can copy this to script `publish.sh` and run it using `./publish.sh <YOUR COMMIT MESSAGE>`

```bash
notablog generate .
rm -rf docs
cp -r public docs
git add .
git commit -m "$1"
git push origin master
``` 

## How to setup custom domain?

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
* Create a `CNAME` record for host `www` to point to value `erajasekar.github.io`. 
* Here is how I have configured it in my namecheap DNS settings.

![Namecheap DNS Settings](https://www.dropbox.com/s/myafmk86z8t3z5g/namecheap-screenshot.png?dl=0&raw=1)

* For more information refer to [this guide](https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-a-subdomain) from github.

## How to Add Google Analytics ?

Google analytics script can be easily added to template html files so that the generated files will contain this code.

```html
<script>
	//COPY AND INSERT CODE FROM YOUR GOOGLE ANALYTICS ADMIN SETUP.
</script>
  ```

## How to make blog SEO friendly ?

To make a site SEO friendly, we need to add `meta` tags in HTML `<head>` section. Notablog already adds most of the meta tags.
The only tag I need to add is `og:image` to provide cover image for social sharing like facebook and twitter.

So I added following lines

```html
{{if(options.siteMeta.cover)}}
  <meta property="og:image" content="{{siteMeta.cover}}">
{{/if}}
``` 

How it looks in metatags io.

![Katranai Thoorum Arivu Social](https://www.dropbox.com/s/6ko9z9csfv61c6v/Katranai%20Social.png?dl=0&raw=1)

* metatags
* tips to share image link and template.
todo - https://github.com/erajasekar/notablog-starter/pull/1/files
* Adding analytics.

## Demo.





