---
layout: post
title: How to Embed Code in your Medium blog or on any Website?
date: 2018-12-24
draft: false
tags: medium blog code programming
comments: true
analytics: true

---

## Problems in direct Medium Embed or Gists

We can display code in Medium by adding code block  between two ``` (s). But this doesn't look pretty without syntax highlighting.

The common alternative is to embed code using github Gists. But, we can't customize syntax highlight theme. Also, it will be nice to annotate code with callouts instead of standard code comments.



## Doculet - Easy way to Embed code in Medium

To solve above problems, I have built a new app (named as  **Doculet**). The beta version of  [Doculet](https://doculet.net/about) is ready to use.

<br>

Doculet can import your existing gists or you can create new code block in Doculet editor. Doculet uses human readable and easy to use [AsciiDoc](https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/#source-code) document markup which provides builtin support for commenting using callouts. 

After you finish editing, you can publish your code for embeding in other sites. 

The step by step instructions are illustrated below.

## Importing Existing Gists 

You can import your Gist by entering Gist Id or URL in Nav header text box as illustrated below.



![Import gist](https://raw.githubusercontent.com/erajasekar/erajasekar.github.io/master/assets/images/doculet-intro/gist-import.gif)



Doculet automatically adds required source code metadata and converts your code to AsciiDoc format. After importing, you can also edit code in Doculet editor.

## Using Doculet editor

In Doculet Editor, you can edit code on left hand side and you will see live preview on the right side. You should use AsciiDoc format for editing which is [very similiar](https://asciidoctor.org/docs/asciidoc-vs-markdown/) to Markdown language. You can simply include source code between two ` - - - -` and define source code language using `[source, <lang>]` above your code like this.

![Import gist](https://raw.githubusercontent.com/erajasekar/erajasekar.github.io/master/assets/images/doculet-intro/doculet-editor.gif)



In addtion, your can use callouts to explain your code. To display callout add `<number>` to the line you want to comment and add explanation using the format `<number> your explanation` below the code like in this example.

![Code callout Example](https://raw.githubusercontent.com/erajasekar/erajasekar.github.io/master/assets/images/doculet-intro/doculet-editor-callout.png)



Refer to [AsciiDoc Quick Reference](https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/#source-code) if you need help with asciidoc syntax. 

## Publishing Your Code

Save your documents when necessary. When your are ready, click on ***publish*** button to share your code for embeding in other sites. You will see links for sharing along with preview of your embed. 

![Share Example](https://raw.githubusercontent.com/erajasekar/erajasekar.github.io/master/assets/images/doculet-intro/share-example3.png){:height="800px" width="850px"}

## Embeding in Medium

In your Meduim editor, simply type URL and hit enter. It will automatically expand into embeded iframe.

![Medium Embed](https://www.dropbox.com/s/52kcrh91qrdsuuj/embed-demo.gif?raw=1)



## Embeding on your blog or any website

To embed Doculet on your blog or any website, copy the iframe code and add to your blog or website. For eg.

```
<iframe src="https://doculet.net/doc/fb1114639d5a47e7b2110c006da4b720"
 align="middle"
 height="650"
 width="100%"
 frameborder="0"></iframe> 
```



## Quickly copy code or switch themes

Readers can quickly copy code by clicking ***copy*** icon. They can also switch between dark or light code theme.

![Switch theme example](https://www.dropbox.com/s/m39wgvi8dagjl7u/theme-select-demo.gif?raw=1)

## Help me improve Doculet

If you find any bugs or have feature request, please submit issue in [Github.](https://github.com/erajasekar/doculet/issues) Please subscribe to [email list](http://eepurl.com/dI-8Ur) to receive updates about the project.



