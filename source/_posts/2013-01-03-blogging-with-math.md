---
layout: post
title: "Blogging with Math: Octopress, MathJax, and Pandoc"
date: 2013-01-03 16:12
comments: true
published: true
external-url: 
categories: [blogging, octopress, mathjax, pandoc, math]
body_id: archive
---

I've been trying to achieve mathematical writing nirvana, as [others][bsag] have [tried before][krautz] me. My hope is to eventually use a single system for all my technical writing, be it for the web or print. Being an experienced LaTeX user, I would expect no less in terms of flexibility and typesetting of mathematical expressions. However, making LaTeX play nice on the web can be a challenge. Here's my solution thus far. 

<!-- more -->

## Configuring Octopress for use with MathJax ##

There's two parts here. The first is getting Octopress to work nicely with [MathJax][MathJax]. This is relatively easy. Octopress has a folder for custom html files. On my install, it's located at

	/source/_includes/custom/

In this folder, find the `head.html` file, and append the following:

	<!--- MathJax Configuration -->
	<script type="text/javascript"
	src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML,http://drz.ac/javascripts/MathJaxLocal.js">
	</script>

This does two things, first it loads MathJax from the MathJax CDN, then loads my custom preferences, which includes a whole slew of macros. [My custom preferences][MathJaxLocal] are placed in the javascript folder,

	/source/javascript/

notice that I need to specify the path to my local configuration in `head.html`, and also at the end of the `MathJaxLocal.js` script itself:

	MathJax.Ajax.loadComplete("http://drz.ac/javascripts/MathJaxLocal.js");

With all this, I should now be able to write some beautiful mathematics, and the result should be rendered with MathJax:
$$
F(\omega) = \int_{-\infty}^\infty f(t) e^{-i \omega t} \d t.
$$

Some may be content with this. However, there were a few other things that troubled me, such as some errors that I would get due to the Markdown processing and the ability to preview my content offline.

## Markdown with MathJax using Pandoc ##

In order to render your Markdown file as HTML, you need a Markdown interpreter. There are several options, rdiscount, kramdown, maruku, multimarkdown, and pandoc are ones that I've tried. Out of the box, Octopress can be easily configured to use either rdiscount, kramdown, or maruku. Being resistant to change, my goal was to be able to write equations exactly how I would in LaTeX. That is, by using the dollar sign characters for inline equations, and double dollar signs for display equations. This is specified in the `MathJaxLocal.js` file. Initially it seemed that maruku handled the interplay with MathJax the best. However, oftentimes things would break. Often if I had an underscore in a math equation, markdown would think the text should be italicized, since that's part of the markdown spec. At the end of this section, I have a test case which would oftentimes not be converted correctly.

As it turns out, [pandoc][pandoc] is a more robust solution for interpreting markdown with mathjax syntax. However, Octopress is not configured to use pandoc out of the box. The first step is to [install the latest version of pandoc][pandocInstall]. Next, we need to figure out how to use pandoc with Octopress. Thanks to [this jekyll plugin][fauno], I was able to get started. Simply place this plugin in your `plugins` directory. The pdf generation wasn't working correctly for me, so I simply stripped out that portion of the code. So my `pandoc.rb` reads

    require 'open3'
    module Jekyll
    # Just return html5
    class MarkdownConverter
    def convert(content)
        flags  = @config['pandoc']['flags']
        output = ''
        Open3::popen3("pandoc -t html5 #{flags}") do |stdin, stdout, stderr|
            stdin.puts content
            stdin.close
            output = stdout.read.strip
        end
        output
        end
    end
	end

Then I needed to change my `_config.yml` as follows:

    markdown: pandoc 
    pandoc:
  	    skip: false
        flags: '--smart --mathjax'

now using the same rake commands, the markdown files are processed by pandoc. One interesting feature about pandoc, that I may discuss in the future, is that it supports the use of bibliographies using BibTeX.         

### Test case ###

This is a test case of markdown / MathJax weirdness.

- The first error is with square brackets. Sometimes they are processed as Markdown and disappear and MathJax incorrectly processes them. 

Example: $y = [z > 0]$. 

- The second error is with underscores. Markdown interprets these as adding emphasis, and hence they break.

Example:

If I have one integral here: 
$$
\int_{-\infty}^\infty f(x) \d x,
$$
and a second integral here
$$
\int_{-\infty}^\infty g(t) \d t, 
$$
we may introduce an issue. 

Hopefully everything is displayed as it should!

## Offline editing ##

With an internet connection, I can use the Octopress preview web host to check out how my draft is progressing. However, once an internet connection is unavailable, the MathJax typesetting breaks since it is essentially loading the configuration I've deployed to render the content I'm previewing. That is, the localhost server loads the MathJax configuration that's actually located at `http://drz.ac/javascripts/MathJaxLocal.js`. So once I don't have wifi available, it can't find this page, and my maths break. 

My ideal solution would be to write my posts in a text editor then preview them offline without requiring the overly complex local webserver. While it's great to see how things look before deploying a post, it can be distracting to deal with when I'm just trying to get my ideas down. 

Enter [Marked][Marked], a companion app for previewing Markdown content. Marked looks for changes in your markdown file, upon a change, converts it to HTML, and displays it in a nice preview window. By default, marked uses multimarkdown. Unfortunately, I would encounter similar issues with MathJax equations that I felt that I should just configure Marked to use pandoc instead. This is aided by using a small bash script as a wrapper for pandoc. 

    #!/bin/bash
    # Wrapper for using pandoc with Marked
    cat - | pandoc -S -f markdown -t html --mathjax

Simply use this script (making sure to `chmod a+x`) as the custom markdown processor in the Marked preferences, and everything should work great. Now to get the equation support, I downloaded the latest version of MathJax and simply keep it in my Dropbox folder (`~/Dropbox/MathJax/`). Within this MathJax folder, I also keep a copy of my `MathJaxLocal.js` script, however one needs to change the last line to

    MathJax.Ajax.loadComplete("file:///users/zac/Dropbox/MathJax/MathJaxLocal.js");

with the appropriate changes for your install. Then when I'm writing offline, I simply include my local MathJax install within the markdown file itself. 

	<script type="text/javascript"
	src="file:///users/zac/Dropbox/MathJax/
	MathJax.js?config=TeX-AMS-MML_HTMLorMML,
	file:///users/zac/Dropbox/MathJax/MathJaxLocal.js">
	</script>

So far, works great!

## Markup Nirvana? ##

For now I'm going to stick with this solution. The only drawback is that I seem to need to always include the javascript to use my local MathJax configuration. It's a little inelegant to have to include it every time, but that's not too much of a headache. On the plus side I now have

1. My Octopress blog configured to use MathJax, 

2. I can seemingly write nearly identically in style to standard LaTeX, and

3. Offline composing is made simple by using Marked. 

[MathJaxLocal]: /javascripts/MathJaxLocal.js "MathJaxLocal.js"

[bsag]: http://rousette.org.uk/blog/archives/pandoc-workflow/ "Pandoc workflow"

[krautz]: http://boolesrings.org/krautzberger/2011/08/03/why-markdown-not-latex/ "Why markdown, not LaTeX?"

[MathJax]: http://www.mathjax.org "MathJax"

[Marked]: http://markedapp.com "Marked"

[pandoc]: http://johnmacfarlane.net/pandoc/ "Pandoc"

[pandocInstall]: http://johnmacfarlane.net/pandoc/installing.html "Pandoc - Installing"
[fauno]: https://github.com/fauno/jekyll-pandoc-multiple-formats "Jekyll pandoc plugin"
