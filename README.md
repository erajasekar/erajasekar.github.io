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


