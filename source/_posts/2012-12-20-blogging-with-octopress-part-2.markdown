---
layout: post
title: "Blogging with Octopress, Part 2"
date: 2012-12-20 23:29
comments: true
published: false
categories: [octopress, blogging]
---

[Last time][BloggingWithOctopress] I discussed the basics of setting up my site using [Octopress][Octopress]. This time I'm going to go into a bit more detail using some of the Ruby scripts that ship with Octopress. 

## Rakefile ##

Rakefiles are the Ruby equivalent of Makefiles. The Rakefile that ships with Octopress has a number of useful scripts for generating new posts and deploying your site.

### YAML front matter ###

The special [YAML Ain't Markup Language front matter][YAMLFrontMatter] tells Octopress how to process your Markdown files. The ``new_post`` script generates this for you. By default the ``published: `` line is omitted. Including ``published: false`` will prevent the post from being deployed, but will show when you preview your site locally with ``rake preview``. This is useful if you like to preview your post in a browser before deploying.

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







[BloggingWithOctopress]: {% post_url 2012-12-19-blogging-with-octopress %} "Blogging With Octopress"

[Octopress]: http://octopress.org/ "Octopress"

[InternalPostLinking]: http://kqueue.org/blog/2012/01/05/hello-world/#internal-post-linking "Internal Post Linking"

[XiWang]: http://kqueue.org "Xi Wang"

[post_url]: https://raw.github.com/michael-groble/jekyll/fix_post_url/lib/jekyll/tags/post_url.rb "post_url Script"

[OctopressBlockquote]: http://octopress.org/docs/plugins/blockquote "Blockquote - Octopress"

[YAMLFrontMatter]: https://github.com/mojombo/jekyll/wiki/yaml-front-matter "YAML Front Matter"