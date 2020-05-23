---
title: Models from BVMs
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

When studying the model theory of set theory, ordinary models are what we really care about. The goal of the technique of forcing is the construction of new legitimate models of ZFC with interesting properties. How can we use $V^{\mathbb{B}}$ to build a new model of ZFC?

## The quotient $V^{\mathbb{B}}/U$

With a BVM of ZFC, every sentence $\phi$ has a truth value $$\| \phi \| \in \mathbb{B}$$, and every sentence provable in ZFC has value 1. Every sentence provably false in ZFC has value 0. Then there might be some sentences with an intermediate truth value $$ \not \in \{0,1\}$$, and these sentences are all independent of ZFC. To obtain a new model of ZFC, we will try and 'collapse' these intermediate truth values to a definite 0 or 1.

Before we define an ultrafilter $U$ on $\mathbb{B}$, we motivate its properties. Suppose $a, b \in \mathbb{B}$ are intermediate truth values satisfying $a \leq b$. If $$\| \phi \| = 

Why you want a filter. Why you want an ultrafilter.

Theorem: the quotient is a model of the language of set theory, and Los' theorem for the model.

If $U \in V$, doesn't do anything. So need something outside the model to make interesting. (Where it comes from is a question for later).

## The extension $V[G]$

Concrete equivalent to the quotient.
Quotient=definitely model, weird to understand.
Extension=conretely built, not obviously a model.

Generic: equal to the quotient. So now not only a model, but a concrete transitive model that extends $V$.

Generic model theorem.

## Quotient as extension

What breaks with the isomorphism when non-generic?

Quotient as a forcing extension of a different base model.

## What of genericity?

The two roles: new set being added, and filter on truth. This is witchcraft and I really don't understand it. Will try and understand it.

So far, the reason we wanted a generic ultrafilter was to make the extension-as-quotient argument work. Is there a way of motivating it as a 'typical set?'. Something tantalasing I noticed: when adjoining a Cohen generic real, the generic real must be normal.