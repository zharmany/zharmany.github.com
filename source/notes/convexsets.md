---
layout: page
title: Convex Sets
comments: false
sharing: false
footer: false
body_id: archive
---
<script type="text/javascript"
src="file:///users/zac/Dropbox/MathJax/
MathJax.js?config=TeX-AMS-MML_HTMLorMML,
file:///users/zac/Dropbox/MathJax/MathJaxLocal.js">
</script>

Convex sets are useful. Here we define them, and show some examples.

<div class="definition">
    A set $C$ is *convex* if for all $x,y \in C$ and for all $\alpha \in [0,1]$ the point $\alpha x + (1-\alpha) y \in C$.
</div>

<div class="definition">
    A function $f:\reals^n \to \reals$ is *convex* if for all $x,y \in \reals^n$, 
    $$
        f(\alpha x + (1-\alpha)y) \le \alpha f(x) + (1-\alpha) f(y)
    $$
    for all $\alpha \in [0,1]$.
</div>


<div class="definition">
    The *$\alpha$-sublevel set* of $f:\reals^n \to \reals$ is the set $C_\alpha = \set{x : f(x) \le \alpha}$.
</div>

<div class="theorem">
    All $\alpha$-sublevel sets of convex functions are convex.
</div>

<div class="proof">
    Let $x$ and $y$ be any two arbitrary points in $C_\alpha$ of $f$. Then we have $f(x) \le \alpha$ and $f(y) \le \alpha$. Let $z = ax + (1-a)y$. From the convexity of $f$ we then have
    $$
    f(z) \le a f(x) + (1-a)f(y) \le \alpha,
    $$
    and hence $z$ belongs to $C_\alpha$
</div>

    



