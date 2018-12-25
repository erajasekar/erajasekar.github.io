---
layout: post
title: How to Embed Code in your Medium blog or on any Website?
date: 2018-12-24
draft: false
tags: medium blog code programming
comments: true
analytics: true

---

*With beautiful syntax highlighting and copy to clipboard support* 

## Problems in direct Medium Embed or Gists

The common method to display code in Medium is to directly add code block  between two ``` . But this doesn't look pretty without syntax highlighting.

The other alternative is to embed code using github Gists. Gists are ok, but we can't customize syntax highlight theme and also can't copy code in a single click. 



## Doculet - Easy way to Embed code in Medium

Because of above problems, I decided to build a new app to make embeding code in Medium or any website easy. The app name is [Doculet](https://doculet.net/about) and beta version is ready to use. 

Doculet can import your existing gists or you can create new code document in Doculet editor. Doculet uses human readable and easy to use [AsciiDoc](https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/#source-code) document markup that is similar to markdown. AsciiDoc provides builtin support to comment code using callouts. 

After you finish editing, you can publish your code for embeding in other sites. 



## Importing Existing Gists 

You can import your Gist by entering Gist Id or URL in Nav header text box.



![Import gist](https://raw.githubusercontent.com/erajasekar/erajasekar.github.io/master/assets/images/doculet-intro/gist-import.gif)



Doculet automatically adds required source code metadata and converts your code to AsciiDoc format.



## Using Doculet editor

In Doculet Editor, you can edit code in left side and see live preview in right side. You should see AsciiDoc format for editing. AsciiDoc format is very similiar to Markdown language and most of the markdown syntax as is works with AsciiDoc. 

You can simply include source code like this:

```
[source,javascript]
.hello.js
----
console.log('Hello World');
----
```



In addtion, your can use callouts to explain your code like this:

```
[source,ruby]
----
require 'sinatra' // <1>

get '/hi' do // <2>
  "Hello World!" // <3>
end
----
<1> Library import
<2> URL mapping
<3> HTTP response body
```



Refer to [AsciiDoc Quick Reference](https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/#source-code) if you need help with asciidoc syntax. Save your documents when necessary.



## Publishing Your Code

When ready, click on publish button to publish your code for embeding in other sites. You will be presented with links to share and preview of your embed. 



![Share Example](https://raw.githubusercontent.com/erajasekar/erajasekar.github.io/master/assets/images/doculet-intro/share-example2.png){:height="800px" width="850px"}

## Embeding in Medium

Simply type URL and hit enter. It will automatically expand into embeded iframe.

![Medium Embed](https://uc9da18d401356e88b0c329a6280.dl.dropboxusercontent.com/cd/0/inline/AYEqbJTiT99zsUMOMBGEE_XdcizBovATWsh1gEM7gdniIqwns2Kwd2T-Y2XC5M-LaaJn9IIpnRs7JwXQBjbAbU6gyXBT9V7Yp4DP_UXQMjs0w5CY1NXb6Jld-bBgOdCKl7etmuyTao0Nigkd2Md4j5YYb5IOsjfNhCGKMYTs81FzQkWEQDrVxM3EcKywVusf-gk/file)



## Embeding on your blog or any website

To embed on your blog or any website, copy the iframe and add to your blog or website. For eg.

```
<iframe src="https://doculet.net/doc/fb1114639d5a47e7b2110c006da4b720"
 align="middle"
 height="650"
 width="100%"
 frameborder="0"></iframe> 
```



## Quickly copy code or switch themes

Readers can quickly copy code by clicking ***copy*** icon. They can also switch between dark or light code theme.

![Switch theme example](https://uc43edce11f4edf2388baab9d42f.dl.dropboxusercontent.com/cd/0/inline/AYHcOzhm5TjngG0ruWj5OYwRniFsu3eym4q-Jg9RlFwjaD5ejudXCyJ3_FIFGMOuRkHxaCMfcwH3z9bvRW5gVzLPYmpxM0HYOf5-rhYmlUhY8HLVX8mXssyZOGIvg7o8A4ywmTzJEeOcu-VoWdDIZk13-eKnaOwCzx8WPlaoJsYQBnllG0jUx1IaB9671kV6fjA/file)





