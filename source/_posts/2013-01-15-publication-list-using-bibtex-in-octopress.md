---
layout: post
title: "Publication List using BibTeX in Octopress"
date: 2013-01-15 17:36
comments: true
external-url: 
categories: [bibtex, octopress]
---

I was looking for a nice way to use BibTeX within Octopress to generate my [list of publications][publications], and came across the [jekyll-citation][jekyllcitation] plugin. 

<!-- more -->

It was fairly easy to setup, first simply install `citeproc-ruby` and `bibtex-ruby` gems by running

    gem install citeproc-ruby
    gem install bibtex-ruby

in the terminal, then add them to your `Gemfile` by adding the two lines:

    gem 'bibtex-ruby'
    gem 'citeproc-ruby'

then you should be set to use them with Octopress. To configure, I grabbed the IEEE format from [the citation style language repository][citationstylelanguage] and placed it in `plugins/ieee.csl`, then I added these lines to `_config.yml`:

    # BibTex Citation plugin
    citation:
        citation_style: plugins/ieee.csl
        citation_locale: en

I was getting an error when using `citation.rb`, and it seems the issue was that it was reading the data as a string and not an array, and hence the `.join` method was failing. So on Line 31 in `citation.rb` I simply changed

      #content = super.join
      content = super

And now it works, no troubles. For instance the example

{% bibtex %}
@article{brothman1991orders,
  title={Orders of value: probing the theoretical terms of Archival Practice},
  author={Brothman, B.},
  journal={Archivaria},
  volume={32},
  number={1},
  year={1991}
}
{% endbibtex %}

was generated using

    {% bibtex %}
    @article{brothman1991orders,
      title={Orders of value: probing the theoretical terms of Archival Practice},
      author={Brothman, B.},
      journal={Archivaria},
      volume={32},
      number={1},
      year={1991}
    }
    {% endbibtex %}

Although it seems that to make a longer list I need to enclose each item in it's own liquid block. So for now, it's not the greatest solution.

[jekyllcitation]: https://github.com/archome/jekyll-citation "jekyll-citation"
[publications]: /publications "Publications"
[citationstylelanguage]: https://github.com/citation-style-language/styles "Citation Style Language"



