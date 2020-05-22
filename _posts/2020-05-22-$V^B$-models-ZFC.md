---
title: $V^{\mathbb{B}}$ models ZFC
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Having defined $V^{\mathbb{B}}$ [here](https://hilbert-spaess.github.io/2020/05/16/Boolean-valued-semantics.html), this post will be a full proof that the axioms of ZFC are valid in this Boolean-valued model. I'm not glossing over the details of this proof because it's one of the main pieces of technical work on the road to forcing. It also can't hurt to go over the statements of the axioms of ZFC again. 

## Canonical names for $V$ in $V^\mathbb{B}$

Recall the definition of $V^{\mathbb{B}}$ as a cumulative hierarchy of 'Boolean-valued sets', and the

## Extensionality and separation

**Extensionality**: $$(\forall x)(\forall y)[(x=y) \Leftrightarrow (\forall z)(z \in x \Leftrightarrow z \in y)]$$. "Sets are determined by their members".

To show that is is valid, we need that for each $x, y \in V^{\mathbb{B}}$, $$\| x = y \| = \bigwedge_{z \in V^{\mathbb{B}}}(\|z \in x\| \Leftrightarrow \| z \in y \|)$$. One direction follows directly from the axioms of first-order logic, so is valid in $V^{\mathbb{B}}$. To get the other direction, it suffices to show that $$ \bigwedge_{z \in V^{\mathbb{B}}}(\|z \in x \| \Rightarrow \| z \in y \|) \leq \| x \subset y \|$$. 

We have that for all $z$, $$y(z) \leq \| z \in x \|$$. So for all $z$,$$(\|z \in x \| \Rightarrow \| z \in y \|) \leq (x(z) \Rightarrow \|z \in y \|$$. Takin