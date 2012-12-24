---
layout: post
title: "Feed Titles in Octopress Linked Lists"
date: 2012-12-21 22:53
comments: true
external-url: 
categories: [octopress, github]
---

I've been experimenting with [linklog customization][link1] using the ``2.1`` branch of Octopress. From what I can tell, there's an error in ``source/_includes/feed_entry.xml``.

<!-- more -->

To get the ``standard_post_marker`` to function correctly a la [Gruber][DaringFireball], where it shows up before the title of his post in the RSS feed, I needed to do some digging.

To fix, I think all that you need to do is switch
{% raw %}
    {% if linklog and site.linklog_marker_position_feed == 'before' %}
    {% unless linklog %}{{ site.standard_post_marker_feed }}{% endunless %}
{% endraw %}

to
{% raw %}
    {% unless linklog %}{{ site.standard_post_marker}}{% endunless %}
    {% if linklog and site.linklog_marker_position_feed == 'before' %}
{% endraw %}

or else the 2nd line in the original can never execute. 

I opened up an issue on the [Octopress GitHub repository][Issue883]. Yay for [OSS][OSS]!

[link1]: http://octopress.org/docs/blogging/linklog/ "Linklog Customization"

[DaringFireball]: http://daringfireball.net "Daring Fireball"

[Issue883]: https://github.com/imathis/octopress/issues/883 "Issue #883"

[OSS]: http://en.wikipedia.org/wiki/Open-source_software "Open source software - Wikipedia"