---
title: Jech Ch14 ("Forcing") solutions
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

I'm writing up some solutions to chapter 14 of Jech's "Set Theory". I don't feel bad about posting these here, as I'm pretty certain that anyone who was otherwise going to buy the book won't not do so on account of this post, whereas for someone who does have access to the book, these have some chance of being useful.

## 14.1 - 14.6: Generic filters on partial orders

These questions are about alternative characterisations of a $V$-generic filter $G$ on a partial order $P$. Recall the standard definition of a generic filter as a filter that intersects every dense subset of $P$ in $V$.

#### 14.2: A filter $G$ on $P$ is $V$-generic if and only if for every $g \in G$, if $D \in V$ is dense below $g$ then $G$ intersects $D$.

$\Rightarrow$: For $g \in G$, if $D \in V$ is dense below $g$ then $$\{p \in P: p \textrm{incompatible with} g \textrm{or} p \in D\}$$ is dense. So it intersects $G$, and since every element of $G$ is compatible with $g$, $G$ intersects $D$.

$\Leftarrow$: Easy, as any dense set is dense below $g \in G$. 

#### 14.3 Generic iff intersects every open-dense subset of $P$

$\Rightarrow:$ obvious.

$\Leftarrow:$ if $D$ is dense then consider the open-dense set $$\{p \in P: \exists d \in D: p \leq d\}$$. This intersects generic $G$, so $G$ intersects $D$ by upward closure of $G$.

#### 14.4: Generic iff intersects every pre-dense subset of $P$.

$\Rightarrow$: Suppose $D$ is predense. Let $\bar{D}$ be the dense closure of $D$. Then $G$ intersects $D$. If $g \in G \cap D$, and $g \not in D$, then $g$ was added as a point of compatibility between $D$ and another element of $P$. So $g \leq d \in D$, and done by upward closure of $G$.

$\Leftarrow$: obvious.

#### 14.5: 