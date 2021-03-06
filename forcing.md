---
title: Forcing
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

I'm working on an expository sequence of posts about the technique of **forcing** in set theory and its use in consistency proofs. Hopefully the sequence will go in a philosophical direction, but this is an area of philosophy for which quite a lot of (thankfully attractive) maths is needed. I'm still a total beginner in this area, so the presentation is probably very naive.

### Intended pre-requisites

- First-order logic up to the completeness theorem
- Basic theory of ordinals
- Axioms of ZFC
- Basic model theory of ZFC (Von Neumann hierarchy, constructible universe)

### Boolean-valued model approach

[Boolean-valued semantics](https://hilbert-spaess.github.io/2020/05/16/Boolean-valued-semantics.html) is an introduction to Boolean-valued models of set theory. It covers Boolean algebras and Boolean-valued models, and defines the standard $\mathbb{B}$-valued model of set theory, $V^{\mathbb{B}}$.

[Models from BVMs](https://hilbert-spaess.github.io/2020/05/23/building-actual-models.html) covers how we can use $V^{\mathbb{B}}$ to obtain new models of ZFC. We consider quotienting by an ultrafilter, and take a first look at forcing extensions, proving the generic model theorem.

[All quotients are extensions](https://hilbert-spaess.github.io/2020/05/24/All-quotients-are-extensions.html) is mostly an exposition of Hamkins' paper on Boolean ultrapowers. We show that $V^{\mathbb{B}}/U$ is always a forcing extension, but the base model is not necessarily $V$. 

[Frameworks for forcing](https://hilbert-spaess.github.io/2020/05/24/forcing-frameworks.html) takes a wider view on what's going on when we adjoin a generic ultrafilter to our base model.

[Independence of CH](https://hilbert-spaess.github.io/2020/05/27/Independence-CH.html) walks through Cohen's proof that the negation of the continuum hypothesis is consistent with ZFC.

[Jech "Forcing" solutions](https://hilbert-spaess.github.io/2020/05/28/Jech-14-solutions.html) has solutions to the exercises from the forcing chapter of Jech's "Set theory", which uses the BVM approach. 