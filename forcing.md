---
title: Forcing
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

I'm working on a sequence of posts about the technique of **forcing** in set theory and its use in consistency proofs. Hopefully the sequence will go in a philosophical direction, but this is an area of philosophy for which quite a lot of (thankfully attractive) maths is needed. I'm still a total beginner in this area, so the presentation is probably very naive.

Intended pre-requisites:
- First-order logic up to the completeness theorem
- Basic theory of ordinals
- Axioms of ZFC
- Basic model theory of ZFC (Von Neumann hierarchy)

[Boolean-valued semantics](https://hilbert-spaess.github.io/2020/05/16/Boolean-valued-semantics.html) is an introduction to Boolean-valued models of set theory. It covers Boolean algebras and Boolean-valued models, and defines the standard $\mathbb{B}$-valued model of set theory, $V^{\mathbb{B}}$.

[$V^{\mathbb{B}}$ models ZFC](https://hilbert-spaess.github.io/2020/05/22/$V-B$-models-ZFC.html) provides the proof that all axioms of ZFC are valid in the standard BVM of set theory. (Still in progress).

[Models from BVMs](https://hilbert-spaess.github.io/2020/05/23/building-actual-models.html) covers how we can use $V^{\mathbb{B}}$ to obtain new models of ZFC. We consider quotienting by an ultrafilter, take and a first look at forcing extensions.