---
title: $V^{\mathbb{B}}$ models ZFC
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Having defined $V^{\mathbb{B}}$ [here](https://hilbert-spaess.github.io/2020/05/16/Boolean-valued-semantics.html), this post will be a full proof that the axioms of ZFC are valid in this Boolean-valued model. I'm not glossing over the details of this proof because it's one of the main pieces of technical work on the road to forcing. It also can't hurt to go over the statements of the axioms of ZFC again. 

## Canonical names for $V$ in $V^\mathbb{B}$

Recall the definition of $V^{\mathbb{B}}$ as a cumulative hierarchy of 'Boolean-valued sets', and the

## Extensionality and separation

**Axiom of extensionality:** $$(\forall x)(\forall y)[(x=y) \Leftrightarrow (\forall z)(z \in x \Leftrightarrow z \in y)]$$.

