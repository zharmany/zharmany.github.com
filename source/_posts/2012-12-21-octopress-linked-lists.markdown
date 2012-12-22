---
layout: post
title: "Octopress Linked Lists"
date: 2012-12-21 17:34
comments: true
external-url: 
categories: [octopress, bogging]
---

The [previous post][MCMRTables] was an example of a Linked List / Linklog post. The characteristics being that the post title links to an external page, and the formatting is slightly different. 

<!-- more -->

It took me a little while to get this feature working in Octopress, as [this post on GitHub][LinklogTest] seems a bit outdated. Thanks to [Neal Sheeran][NealSheeran] for [his post][LinkedListPosts] suggesting to use the ``2.1`` branch instead of the ``linklog-test`` branch. After pulling that branch and merging conflicts I was able to get things working properly.

A last note, there are some [configuration options][OctopressLinklog] for changing the style of the linked list posts. At some point I'll have to decide on what side of the Gruber/Armet line I fall. For now I'll stick with the defaults.


[MCMRTables]: {% post_url 2012-12-21-multi-column-and-multi-row-cells-in-latex-tables %}

[LinklogTest]: https://gist.github.com/1812265 "How to test Octopress' linklog feature"

[NealSheeran]: http://www.nealsheeran.com "Neal Sheeran"

[LinkedListPosts]: http://www.nealsheeran.com/archives/2012/09/linked-list-posts-mt-to-octopress/ "Linked List Posts: From Movable Type to Octopress"

[OctopressLinklog]: http://octopress.org/docs/blogging/linklog/ "Writing a Linklog - Octopress"

