---
title:  "Building my site with jekyll and bootstrap on github pages"
date:   2014-12-31 21:00:00
categories: technology
tags: cms web git
---


I have been very much involved into new top level domain names like .guru, .ninja, .dance, .services, .software and so I bought couple of them just to get a taste of it. For example, chirag.software.

Now, what do I do with it? Buy hosting, spend some money Recurrently!. I came to know about [Github Pages][github-pages] which will host static sites for free. I liked the idea of free, but it definitely seemed cumbersome and waste of time to go back to old ages. For me, there has to be some programming and cool technology involved for me to get excited and do it.

I ran into [jekyll][jekyll] in github pages documentation. It basically allows us to write simple markdown content and pre-compiles it into static pages. This pre-compile mechanism allows us to manage css, templates, layouts very easily with re-use. 

I was getting more and more curious. I was also new to git so I thought about just getting started and try it out!

**The setup:**

* [Jekyll 2.5.3][jekyll]
* [Bootstrap sass 3.3.1][bootstrap-sass]
* [Github pages][github-pages]

#### Get and start jekyll

{% highlight sh %}
$ gem install jekyll
$ jekyll new my-awesome-site
$ cd my-awesome-site
~/my-awesome-site $ jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

I immediately added this base code to a git repository so that I get version control and history.

#### Get bootstrap sass and integrate with to jekyll


I downloaded [sass][bootstrap-sass] and added to jekyll config.

From the downloaded sass folder to jekyll:

* copied assets/fonts, assets/images, assets/javascripts directories into /assets directory.
* copied full assets/stylesheets/bootstrap folder into /_sass directory.
* copied main sass files from assets/stylesheets into /_sass directory.
* copied bootstrap/_variables sass file into /_sass directory to manually import in correct order.
* removed reference to bootstrap/_variable sass file from _bootstrap sass file as it will be imported in main sass to achieve necessary ordering.
* imported bootstrap sass into jekyll sass to integrate and it looked as show below when I finished.

In the main.scss file of jekyll:

{% highlight sass %}

// importing bootstrap variables file early so that those variables can be used in 
// defining out variables down below before importing jekyll scss files which use these variables.
@import 
	"bootstrap_variables",
	"bootswatch_flatly_variables"
;

// -- define variables here --
$base-font-family: $font-family-base;

// Import partials from `sass_dir` (defaults to `_sass`)
@import
        "base",
		"bootstrap",
		"bootswatch_flatly",
		"layout",
		"syntax-highlighting"
;
{% endhighlight %}

I left jekyll's sass because I still planned to use some of the styles defined there which were particularly for blog posts.
I just changed the jekyll defined custom variable values to bootstrap values.
I will explain bootswatch_flatly below.

The folder structure would look as shown in the screenshot:
![bootstrap sass integrated into jekyll]({{ site.url }}/assets/images/jekyll-bootstrap-sass-folder-view.png){: .pull-right style="width: 278px; height: 456px; padding: 5px; 0px 5px; 15px;"}

In order to reference from HTML,

* added main.css into head include file.
* added bootstrap and jquery js into footer include file.
* added bootstrap navbar (top navigation bar) in the header include file.

#### Bootstrap theme

I downloaded a free theme [flatly](http://bootswatch.com/flatly/).

I just had to copy the _variables.scss and _bootswatch.scss into the main _scss directory.

You can already see that in the screenshot and in the import statements above. I renamed it for the names to provide more context and distinction.

#### Comments for the blog

I signed up for disqus. It provided an html/javascript universal code snippet to add to the site.

I added the snippet to my post layout so that it becomes part of every blog post by default.

I have added a front-matter variable and site wide _config.yml variable to be able to disable it easily at any level.

#### Re-using this base setup

I have established this base setup at following git repository.

[Jekyll base site with bootstrap - source code](https://github.com/cdpatel/chirag-jekyll-src)

I plan to maintain that base for any new web site that I may want to build.

* I initialized an empty repository for my github pages site. 
* I added the above mentinoed base source repository as remote.
* And pulled from the source remote to import all the base source code.

I will continue to operate from github pages repository for any content changes like adding blog posts. I may add infrastructural changes like bootstrap upgrade or a tag cloud into the base source site and pull into my github pages repository.

Feel free to use the base setup.

[github-pages]: http://pages.githuh.com
[jekyll]:      http://jekyllrb.com
[bootstrap-sass]: http://getbootstrap.com/getting-started/
