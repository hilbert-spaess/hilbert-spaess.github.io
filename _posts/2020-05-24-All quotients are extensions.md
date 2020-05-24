---
title: All quotients are extensions
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

We [previously](https://hilbert-spaess.github.io/2020/05/23/building-actual-models.html) saw that if $\mathbb{B}$ is a Boolean algebra, and $U$ is an ultrafilter, then $V^{\mathbb{B}}$ is a model of ZFC. Further, if $U$ is $V$-generic, then $V^{\mathbb{B}}/U$ is isomorphic to $V[U]$, the forcing extension of $V$ by $U$. As an aside to the main expository plotline, it's interesting to see how the isomorphism breaks down in the case that $U$ isn't generic, and what the appropriate generalisation is. The presentation and ideas here are mostly based on work by [Hamkins](https://arxiv.org/abs/1206.6075), although the proofs are slightly different.

## $\breve{V}, \hat{V}$, and $\breve{V}_U$

Recall that each each set $x \in V$ has a canonical name $\breve{x} \in V^{\mathbb{B}}$. We define the name-class $\breve{V}$ via $$\| x \in \breve{V}\| = \bigvee_{y \in V}\| x = \breve{y}\|$$. Let $x_1, ..., x_n \in V$. Then it's a simple inductive proof to see that $$V \models \phi(x_1, ..., x_n) \Leftrightarrow \|\phi^{\breve{V}}(\breve{x_1}, ..., \breve{x_n})\| = 1$$. But we can construct $x \in V^{\mathbb{B}}$ such that $$\| x \in \breve{V}\| = 1$$, even though $x$ is not the canonical name of a set in $V$. If $\mathbb{B}$ is non-trivial, we can find a set of values $A \subseteq \mathbb{B}$  with disjunction 1, even though none of the values is itself 1. If, for example $$\| x = \breve{a} \| = a$$ for all $a \in A$, then $x$ is a sort of 'superposition' of canonical names, but is not itself a canonical name. For this reason, it is misleading to think of $\breve{V}$ as a class of canonical names.

Let $$\hat{{V} = \{x \in V^{\mathbb{B}}: \| x \in \breve{V}\| = 1\}$$. 



## $V^{\mathbb{B}}/U$ is a forcing extension