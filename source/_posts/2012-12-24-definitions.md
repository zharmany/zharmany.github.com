---
layout: post
title: "Definitions"
date: 2012-12-24 02:38
comments: true
published: false
external-url: 
categories: [math]
---

Over the past several months, I've been on a quest to sure up some of the missing gaps in my knowledge of fundamental mathematics. If you are, like myself, an engineer or physicist by training, it may take you a bit of time to apprecaite the importance of *definitions* when approaching pure mathematics.

<!-- more -->

In engineering classes, you can get by describing a concept by just showing a few examples. This usually suffices for the purposes of putting the mathematics to good use. That is, you want to deliver the message, "this thing I just talked about, it's useful, here's how."

## An example ###

The best example I can think of is the Dirac delta function. The way it's usually motivated is to think of a unit energy pulse. Any shape will do, but for the sake of argument, let's define a pulse $p$ of duration $T$ as 
$$ 
p_T(t) =
\cases{
1/T & $|t|, \le T/2$;\cr
0 & $|t|, > T/2$.}
$$
If we define the energy of a pulse $p$ as 
$$
E(p) = \int_{-\infty}^\infty \abs{p(t)} \dd t, 
$$
we see that $E(p_T) = 1$, regardless of $T$. Now we think of an idealized infinitesimal pulse and call that $\delta$. We think of simply taking the limit [^LimitAside]
$$
\delta = \lim_{T \to 0} p_T. 
$$

[^LimitAside]: The more mathematical of you may be thinking about this limiting process. For instance, if $p_T$ belongs to some function class, this class needs to be closed in order for $\delta$ to also be a member of this function class. Yes, this is one of the difficulties in defining $\delta$, but I'm glossing over this for right now. 

With this approach of explaining how we arrive at $\delta$, we come to the conclusion that we must simultaneously have that $\delta(t) = 0$ for all $t \ne 0$, and 
$$
\int_{-\infty}^\infty \delta(t) \dd t = 1.
$$
This typically doesn't jive with the student's previous math classes when they learned integration. Changing the value of the integrand at a single point does not affect the value of the integral, it should be true that
$$
\int_{-\infty}^\infty 0 \dd t = \int_{-\infty}^\infty \delta(t) \dd t = 0.
$$
The next line is usually the hardest to swallow, "Well, the value of $\delta(0)$ is now *infinitely big*, which fixes everything, you see!" So, in the student's mind, he's thinking that a sensible definition of $\delta$ would be to say
$$
\delta(t) = \cases{ + \infty, & $t = 0$; \cr 0, & $t \ne 0$.}
$$
As engineers, we don't ponder about how nonsensical this really is, because we immediately switch into *application mode*, where we ask "how is this used?". We don't necessarily need to have a firm grasp of the concept in order want to see it in action. We're the same cadre who used to lick 9V batteries. 

## Applications ##

Usually we get taught one of two things next, either the sampling property of $\delta$, or its relation to the unit-step function. I'll touch on the former. The key idea is that *both* rely on using $\delta$ within an integral. Usually before this class, the professor would have defined an inner product of two signals,
$$
\inner{x}{y} := \int_{-\infty}^\infty x(t) \ y(t) \dd t.
$$
So what hapens when we take the inner product with a $\delta$? The argument is usually something like this:

$$
\inner{x}{\delta} 
 = \int_{-\infty}^\infty x(t) \ \delta(t) \dd t 
 = \int_{-\infty}^\infty x(0) \ \delta(t) \dd t 
 = x(0) \int_{-\infty}^\infty \ \delta(t) \dd t = x(0).
$$
The argument for the second equality is that since $\delta$ is zero everywhere except zero, we might as well just replace $x(t)$ with $x(0)$. Next, we just use the unit energy property of $\delta$. **Neat**: inner products with $\delta$ return the value of the signal at zero. 

## Back to definitions ##

At the end of the lecture, this may convince the student that this is useful, and that $\delta$ lets us do some interesting things, like taking discrete samples of a signal. However, trouble arises when the student may revisit his notes. For example, if the student is asked on an assignment to compute $\inner{x}{2\delta}$, he may go back to the "definition" that
$$
\delta(t) = \cases{ + \infty, & $t = 0$; \cr 0, & $t \ne 0$,}
$$
and conclude that since $ +\infty \cdot 2 = \infty$, it should be true that $2 \delta = \delta$, and we should expect the same answer of $x(0)$. No, you see poor student, the pulse at the origin is really *twice* infinitely big, and the correct answer is $2 x(0)$. 







