---
layout: post
title: "Valid XML Atom Feed on GitHub Pages"
date: 2012-12-22 00:59
comments: true
external-url: 
categories: 
---

Attempting to brand my site, I wanted to use &#x24e9; to prepend the post title when the entry was not a linklog item. This wound up breaking the atom feed in [Google Reader][GoogleReader], and hence my favorite Google Reader client [Reeder][Reeder]. I couldn't have that.

<!-- more -->

The strange thing was that Firefox displayed everything correctly, but Google Reader and hence Reeder simply showed ``&#x24e9;`` in place of the correct unicode symbol. As it turns out, the feed is encoded as ``utf-8``, however [GitHub Pages][GitHubPages] was serving the file as ``US-ASCII``, causing the issue. 

Thanks to [Taylor Fausak][TaylorFausak]'s [post on serving atom feeds at GitHub][ServingAtom], I was able to come up with a solution. Simply using the extension ``.atom`` will make GitHub serve the correct headers. Rather than use the redundant ``atom.atom``, I elected to shoot for ``feed.atom``. To do this in [Octopress][Octopress] was fairly straightforward.

1. In ``_config.yml``, I changed ``subscribe_rss: /atom.xml`` to ``subscribe_rss: /feed.atom``. I thought this would be enough. I was wrong.

2. In the ``Rakefile``, ``plugins/category_generator.rb``, and ``sitemap_generator.rb``, search and replace ``atom.xml`` with ``feed.atom``. (Strange these guys are hard coded).

3. In the ``source`` directory, rename ``atom.xml`` to ``feed.atom``.

Now I have a [W3C certified valid feed][W3C] and everything works splendidly. That is, until I break something new.



[GoogleReader]: http://reader.google.com "Google Reader"

[Reeder]: http://reederapp.com/ "Reeder"

[GitHubPages]: http://pages.github.com "GitHub Pages"

[Octopress]: http://octopress.org/ "Octopress"

[TaylorFausak]: http://taylor.fausak.me/ "Taylor Fausak"

[ServingAtom]: http://taylor.fausak.me/2012/04/26/serving-atom-feeds-with-github-pages/ "Serving Atom Feeds with GitHub Pages"

[W3C]: http://feed2.w3.org/check.cgi?url=http%3A//drz.ac/feed.atom "Feed Validator Results: http://drz.ac/feed.atom"