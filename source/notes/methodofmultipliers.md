---
layout: page
title: Method of Multipliers and ADMM
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

# The Method of Multipliers #

Solves the prototype problem
$$
    \ConMinProb{x \in \reals^n}{f(x)}{Ax=b}
$$
with the following algorithm:
$$
\begin{aligned}
x^{k+1} &:= \argmin_x L_\rho (x, y^k) \\
y^{k+1} &:= y^k + \rho(Ax^{k+1} - b) 
\end{aligned}  
$$
where 
$$
L_\rho(x,y) := f(x) + y^\T (Ax - b) + \frac{\rho}{2} \twonorm{Ax - b}^2
$$
The precise form of the update is motivated by the desire to maintain dual feasibility. The KKT conditions for the original problem are
$$
\begin{aligned}
\grad f(x^\star) + A^\T y^\star &= 0 \\
Ax^\star &= b.
\end{aligned}
$$
So we desire $\grad f(x^{k+1}) + A^\T y^{k+1} = 0$. Since $x^{k+1}$ optimizes $L_\rho(x,y^k)$, we have that
$$
\grad L_\rho(x^{k+1}, y^k) = \grad f(x^{k+1}) + A^\T y^k + \rho A^\T (A x^{k+1} - b) = 0.
$$
From this, we have
$$
\grad f(x^{k+1}) + A^\T y^{k+1} = A^\T \left[ y^{k+1} - (y^k + \rho (A x^{k+1} - b))\right]
$$
which will be zero if we select $y^{k+1} = y^k + \rho(Ax^{k+1} - b)$.

Since the iterates are always dual feasible, a way to monitor the convergence of the algorithm is to examine the primal feasibility ($Ax = b$), a common choice is to simply examine $\twonorm{Ax^{k}-b}$.

