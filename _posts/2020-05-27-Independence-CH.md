---
title: Independence of the Continuum Hypothesis
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Cohen generic reals

I'll go into more detail elsewhere, but before we can define Cohen generic reals, we need to do a quick recap of generic filters on arbitrary partial orders. Any partial order $(P, \leq)$ can be embedded densely into a Boolean algebra $B(P)$. Now, given a generic filter $G \subset P$ (a filter that intersects all dense filters on $P$), the set $$H = \{b \in B(P): \exists g \in G: e(g) \leq b\}$$ is a generic ultrafilter on $B(P)$. Further, $G$ and $H$ are constructible from one another. We can thus use $V[G]$ and $V[H]$ interchangeably. Strictly speaking, we only know how to define $V[H]$ by interpretation, but this equals $V[G]$ in the sense that it is the smallest model of ZFC that contains both $V$ and $G$. We can thus assume that we can extend a set-theoretic universe by a generic filter on an arbitrary partial order. A partial order used in this manner is a **notion of forcing**.

Let $V$ be a transitive model of ZFC. Let $(P, \leq) \in V$ be the notion of forcing consisting of all functions $$f : \omega \to \{0,1\}$$ with finite domain, ordered under extension (ie $f \leq g$ if and only if $g \subset f$). Considered as a 'set of truth values' , we see that longer sequences in $P$ are more stringent notions of truth. Considered as 'raw material' for an extension of $V$, the partial order consists of approximations to elements of $\mathcal{P}(\omega)$. Note that $p, q \in P$ are compatible only if they have a mutual refinement- so one must be a refinement of the other. So a filter $G$ either consists of a finite 0-1 sequence and all its coarsenings, or else consists of all finite approximants to an element of $\mathcal{P}(\omega)$. 

Single Cohen generic real.

Sets of Cohen generic reals.

The proof, as long as cardinals are preserved.

## Cardinals preserved

Proof using countable chain condition.

Proof of countable chain condition.