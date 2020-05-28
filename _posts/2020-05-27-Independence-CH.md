---
title: Independence of the Continuum Hypothesis
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

The continuum hypothesis is the claim that $2^{\aleph_0} = \aleph_1$ is a theorem of ZFC. The consistency of CH with ZFC was established by Godel using the inner model $L$. To prove the consistency of $\lnot$CH with ZFC, we attempt to add more elements to $\mathcal{P}(\omega)$, until we can construct an injection from $\omega_2$. Provided we haven't messed up the fact that $\| \omega_2 \| = \aleph_2$, CH is false in this new model of ZFC. There are therefore two key steps to the proof. The first is to find a Boolean algebra such that a generic ultrafilter facilitates the construction of new elements of $\mathcal{P}(\omega)$. The second is to check that we haven't messed up the cardinals of our base model in the process of adjoining new reals. 

## Cohen generic reals

I'll go into more detail elsewhere, but before we can define Cohen generic reals, we need to do a quick recap of generic filters on arbitrary partial orders. Any partial order $(P, \leq)$ can be embedded densely into a Boolean algebra $B(P)$. Now, given a generic filter $G \subset P$ (a filter that intersects all dense filters on $P$), the set $$H = \{b \in B(P): \exists g \in G: e(g) \leq b\}$$ is a generic ultrafilter on $B(P)$. Further, $G$ and $H$ are constructible from one another. We can thus use $V[G]$ and $V[H]$ interchangeably. Strictly speaking, we only know how to define $V[H]$ by interpretation, but this equals $V[G]$ in the sense that it is the smallest model of ZFC that contains both $V$ and $G$. We can thus assume that we can extend a set-theoretic universe by a generic filter on an arbitrary partial order. A partial order used in this manner is a **notion of forcing**.

Let $V$ be a transitive model of ZFC. Let $(P, \leq) \in V$ be the notion of forcing consisting of all functions $$f : \omega \to \{0,1\}$$ with finite domain, ordered under extension (ie $f \leq g$ if and only if $g \subseteq f$). Considered as a 'set of truth values' , we see that longer sequences in $P$ are more stringent notions of truth. Considered as 'raw material' for an extension of $V$, the partial order consists of approximations to elements of $\mathcal{P}(\omega)$. Note that $p, q \in P$ are compatible only if they have a mutual refinement- so one must be a refinement of the other. So a filter $G$ either consists of a finite 0-1 sequence and all its coarsenings, or else consists of all finite approximants to an element of $\mathcal{P}(\omega)$. A generic filter $G$ must be the latter, since for all $n \in \omega$, it intersects the dense set $$D_n = \{f \in P: n \in \textrm{dom}(f)\}$$.

We are now working in $V[G]$, the forcing extension of $V$ with respect to the notion of forcing $P$ (if you're confused about why I'm not requiring countability of $V$, check [this post](https://hilbert-spaess.github.io/2020/05/24/forcing-frameworks.html)). We have shown previously that $V[G]$ has the same ordinals as $V$, so in particular $\mathcal{P}(\omega)^V = \mathcal{P}(\omega)^{V[G]}$. With $G$ as above, we note that $\cup G$ is an element $\alpha$ of $\mathcal{P}(\omega)$ in $V[G]$. Further, $\alpha \not in V$, for otherwise $G$ would not intersect the dense set $$\{f \in P: f \not \subseteq \alpha\}$$. Thus we have succeeded in adjoining to $V$ a new element of the powerset of $\omega$. The element adjoined in this manner is called a **Cohen generic real**.

For the proof sketched in the introduction, we don't just want a single new real, but a whole set. The notion of forcing $(P, \leq)$ in this case is the set of functions $f$ with domain a finite subset of $\omega_2 \times \omega$ and codomain $$\{0,1\}$$, partially ordered by inclusion as above. A generic ultrafilter consists of all finite approximants to a full function $$f : \omega_2 \times \omega \to \{0,1\}$$. We obtain a function from $\omega_2$ to $\mathcal{P}(\omega)$. We need to check that this function is an injection ("the new reals are all distinct"). 

The proof, as long as cardinals are preserved.

## Cardinals preserved

Proof using countable chain condition.

Proof of countable chain condition.