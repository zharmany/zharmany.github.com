---
layout: post
title: "Matching Content to MathJax"
date: 2013-01-14 18:15
comments: true
external-url: 
categories: [MathJax, Octopress]
---

[MathJax][MathJax] is great, but one small annoyince is when using plain text within an equation (with the `\text{}` command), the typeface would not match the surrounding content. If you like the MathJax typeface, the easiest way to solve this subtle problem is to use the MathJax typeface for your content. 

<!-- more -->

In [Octopress][Octopress], this is fairly straightforward to do, thanks to [this post][FontUsage], the bit of CSS one needs is

    @font-face {
        font-family: 'MJX_Main';
            src: url('http://cdn.mathjax.org/mathjax/latest/fonts/HTML-CSS/TeX/eot/MathJax_Main-Regular.eot'); /* IE9 Compat Modes */
            src: url('http://cdn.mathjax.org/mathjax/latest/fonts/HTML-CSS/TeX/eot/MathJax_Main-Regular.eot?iefix') format('eot'),
                url('http://cdn.mathjax.org/mathjax/latest/fonts/HTML-CSS/TeX/woff/MathJax_Main-Regular.woff')  format('woff'),
                url('http://cdn.mathjax.org/mathjax/latest/fonts/HTML-CSS/TeX/otf/MathJax_Main-Regular.otf')  format('opentype'),
                url('http://cdn.mathjax.org/mathjax/latest/fonts/HTML-CSS/TeX/svg/MathJax_Main-Regular.svg#MathJax_Main-Regular') format('svg');
    }

Since Octopress uses [Sass][Sass], this is best placed in `/sass/custom/_styles.scss`. I simply appended the code to the end. This defines a font-family `MJX_Main`, which we can use for our serif styling by adding

	$serif: "MJX_Main", serif;

to `/sass/custom/_fonts.scss`. 

So now the typeface used in this post will match that used in equations. For example, when I define $\ind{A}$ as the binary indicator function of the event $A$:
$$
	\ind{A} = \cases{
		1 & if $A$ is true,\cr
		0 & otherwise,}
$$
the ``otherwise'' here is the same as in the equation. This makes the math a bit more seamless. It seems that going the opposite direction (styling MathJax to match your content) may be a bit more difficult. 


[MathJax]: http://www.mathjax.org "MathJax"

[Octopress]: http://octopress.org/ "Octopress"

[Sass]: http://sass-lang.com/ "Sass"

[FontUsage]: https://groups.google.com/forum/?fromgroups=#!topic/mathjax-users/jqQxrmeG48o "MathJax Users Google Group"
