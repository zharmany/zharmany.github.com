---
layout: post
title: "Blogging with Octopress, Part 2"
date: 2012-12-20 23:29
comments: true
published: true
categories: [octopress, blogging]
---

[Last time][BloggingWithOctopress] I discussed the basics of setting up my site using [Octopress][Octopress]. This time I'm going to go into a bit more detail using some of the Ruby scripts that ship with Octopress. 

<!-- more -->

## Rakefile ##

Rakefiles are the Ruby equivalent of Makefiles. As detailed on [the Octopress site][BloggingBasics], the Rakefile that ships with Octopress has a number of useful scripts (rake tasks) for generating new posts and deploying your site.

### New Posts ###

Generating a new post is as simple as 

    rake new_post["title"]

which creates a new Markdown file in your ``source/_posts`` directory with filename given by the title, prepended by the date. This will already contain useful metadata that Octopress uses (see the YAML front matter section below). Simply edit this Markdown file to fill your post with content. 

### New Pages ###

I haven't added any new pages quite yet, but there is a rake task for creating new pages easily:

	rake new_page[filename]

This will create the file ``source/filename/index.markdown`` that will ultimately be served as ``filename/index.html`` on your website.

### Preview, Generate, and Deploy ###

To use a local webserver to serve all your posts (including ones with the ``published: false`` flag), simply run

	rake preview

and point your browser to ``http://localhost:4000``. One trick that made using this server a bit easier is to use [Fluid][Fluid] to create an "Octopress Preview" app. Note that to get MathJax (the subject of a future post) working correctly, I needed to change the User Agent to Safari, otherwise it didn't seem that it handled JavaScript correctly. 

If you're satisifed with your site, you can generate the html files and deploy it to GitHub Pages by running

	rake generate
	rake deploy

Very slick.	

### Don't forget to commit and push your source! ###

Lastly, the beauty of having your site as the ``master`` branch, and everything else as the ``source`` branch is that you can modify your website and use version control without having to publish all your changes. Once you've made a new post or page, or some other tweaks to your page source, simply run 

	git add .
	git commit -m 'your message'
	git push origin source

and your progress will be saved on GitHub.	


### YAML front matter ###

The special [YAML Ain't Markup Language front matter][YAMLFrontMatter] tells Octopress how to process your Markdown files. The ``new_post`` script generates this for you. By default the ``published: `` line is omitted. Including ``published: false`` will prevent the post from being deployed, but will show when you preview your site locally with ``rake preview``. This is useful if you like to preview your post in a browser before deploying.

### Below the fold ###

If you want to restrict the amount of a post that is shown in your blog index, simply insert the
	
	<!-- more -->

tag into your post. The remainder of the post will not be shown in the blog index.

## Plugins ##

The ``plugins`` directory contains some usful scripts. Here I'll show a few examples. 

### Blockquotes ###

Standard Markdown blockquotes, coded as

    > Don't Panic.   
    > **Douglas Adams** - The Hitchhiker's Guide to the Galaxy

appears as

> Don't Panic.  
> **Douglas Adams** - The Hitchhiker's Guide to the Galaxy

which is perfectly fine. However, using the ``blockquote`` script, they appear a bit more fancy:

{% blockquote Douglas Adams, The Hitchhiker's Guide to the Galaxy %}
Don't Panic.
{% endblockquote %}

This was created using

    {% blockquote Douglas Adams, The Hitchhiker's Guide to the Galaxy %}
    Don't Panic.
    {% endblockquote %}

This environment is especially nice for linking to quotes in articles. [See the documentation][OctopressBlockquote] for usage details.
    

### Internal post linking ###

Thanks to [Xi Wang][XiWang]'s post about [internal post linking][InternalPostLinking], I was able to use his linked ``post_url`` script to more easily make internal links to posts in this blog. Simply download [post_url.rb][post_url] and place it into your ``plugins`` directory.

I used this code at the beginning of the post to generate the URL:

    {% post_url 2012-12-19-blogging-with-octopress %}

Here ``2012-12-19-blogging-with-octopress`` is the name of the Markdown file (sans extension, of course) that I used to generate the previous post. Full disclosure, I used the Markdown syntax:

    [Last time][BloggingWithOctopress]

    [BloggingWithOctopress]: {% post_url 2012-12-19-blogging-with-octopress %} "Blogging With Octopress"

[BloggingBasics]: http://octopress.org/docs/blogging/ "Blogging Basics - Octopress"

[BloggingWithOctopress]: {% post_url 2012-12-19-blogging-with-octopress %} "Blogging With Octopress"

[Octopress]: http://octopress.org/ "Octopress"

[InternalPostLinking]: http://kqueue.org/blog/2012/01/05/hello-world/#internal-post-linking "Internal Post Linking"

[XiWang]: http://kqueue.org "Xi Wang"

[post_url]: https://raw.github.com/michael-groble/jekyll/fix_post_url/lib/jekyll/tags/post_url.rb "post_url Script"

[OctopressBlockquote]: http://octopress.org/docs/plugins/blockquote "Blockquote - Octopress"

[YAMLFrontMatter]: https://github.com/mojombo/jekyll/wiki/yaml-front-matter "YAML Front Matter"

[Fluid]: http://fluidapp.com "Fluid"