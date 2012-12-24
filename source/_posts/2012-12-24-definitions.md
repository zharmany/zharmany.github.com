---
layout: post
title: "Definitions"
date: 2012-12-24 02:38
comments: true
published: false
external-url: 
categories: [math]
---

Over the past several months, I've been on a quest to sure up some of the missing gaps in my knowledge of fundamental mathematics. If you are, like myself, an engineer or physicist by training, one of the most difficult things to get accustomed to when approaching pure mathematics is the importance of *definitions*. In engineering classes, you can get by describing a concept by just showing a few examples. This usually suffices for the purposes of putting the mathematics to good use. That is, you want to deliver the message, "this thing I just talked about, it's useful, here's how."

The best example I can think of is the Dirac delta function. The way it's usually motivated is to think of a unit energy pulse. Any shape will do, but for the sake of argument, let's define a pulse $p$ of duration $T$ as 
$$ 
p_T(t) =
\cases{
1/T & $|t|, \le T/2$;\cr
0 & $|t|, > T/2$.}
$$
If we define the energy of a pulse $p$ as 

$$
E(p) = \int_{-\infty}^\infty \abs{p(t)} dt, 
$$

we see that $E(p_T) = 1$, regardless of $T$. Now we think of an idealized infinitesimal pulse and call that $\delta$. We think of
$$
\delta = \lim_{T \to 0} p_T.
$$
With this definition, we have that $\delta(t) = 0$ for all $t \ne 0$.
