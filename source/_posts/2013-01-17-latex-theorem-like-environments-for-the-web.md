---
layout: post
title: "LaTeX Theorem-like Environments for the Web"
date: 2013-01-17 06:41
comments: true
external-url: 
categories: [latex, css, mathjax]
---

Although MathJax offers LaTeX-like mathematical typesetting for the web, there are some other constructs from LaTeX that would be useful for a mathematical blog. For instance, the `amsthm` package allows you to define environments for theorems, proofs, lemmas, definitions, and so on. However, MathJax doesn't implement these higher-level formatting features. And rightly so; any formatting on the web should be done with CSS. 

<!-- more -->

Looking to see if anyone has attacked this problem, I came across [Samuel Coskey's post][SamuelCoskey] where he suggests using custom HTML tags as a solution. However, it [seems to be][SO1] a [bad idea][SO2] to use custom HTML tags. A more robust solution would be to use custom CSS classes instead. 

The CSS I'm using is in `theorems.css` below. If you prefer an open [Halmos / QED][QED] symbol versus the closed symbol, use `\25FB` in place of `\25FC`. 

{% include_code css/theorems.css Theorem-like Environments %}

If you happen to be using Octopress, which uses [Sass][Sass], this code can be appended to `/sass/custom/_styles.scss`.

And now to see this in action. The markdown (with inline HTML)

{% include_code md/theoremsexample.md Definition Example lang:html %}

will produce the following:

<div class="definition">
A set $C$ is *convex* if for all $x,y \in C$ 
and for all $\alpha \in [0,1]$ the point 
$\alpha x + (1-\alpha) y \in C$.
</div>

<div class="theorem">
There are no natural numbers $\naturals = (1, 2, 3, \ldots)$ 
$x$, $y$, and $z$ such that $x^n + y^n = z^n$,
in which $n$ is a natural number greater than 2.
</div>

One improvement would be to allow theorem names and numbering (with subsequent referencing), but I think for now this is a nice solution.

[SamuelCoskey]: http://boolesrings.org/scoskey/writing-math-on-the-web/ "Writing math on the web"
[SO1]: http://stackoverflow.com/questions/5970093/using-custom-html-tags "Using custom HTML tags"
[SO2]: http://stackoverflow.com/questions/211394/when-to-use-custom-html-tags "When to use custom HTML tags"
[QED]: http://en.wikipedia.org/wiki/Q.E.D. "Q.E.D. - Wikipedia"
[Sass]: http://sass-lang.com/ "Sass"