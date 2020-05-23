---
title: Models from BVMs
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

When studying the model theory of set theory, ordinary models are what we really care about. The goal of the technique of forcing is the construction of new legitimate models of ZFC with interesting properties. How can we use $V^{\mathbb{B}}$ to build a new model of ZFC?

## The quotient $V^{\mathbb{B}}/U$

With a BVM of ZFC, every sentence $\phi$ has a truth value $$\| \phi \| \in \mathbb{B}$$, and every sentence provable in ZFC has value 1. Every sentence provably false in ZFC has value 0. Then there might be some sentences with an intermediate truth value $$ \not \in \{0,1\}$$, and these sentences are all independent of ZFC. To obtain a new model of ZFC, we will try and 'collapse' these intermediate truth values to a definite 0 or 1. The most straightforward strategy for carrying out such a collapse is to pick a subset $U \subset \mathbb{B}$. Then we will try to ensure that $\phi$ is true in our collapsed model if and only if $$\| \phi \| \in U$$.

Suppose $a, b \in \mathbb{B}$ are intermediate truth values satisfying $a \leq b$. If $$\| \phi \| = a$$, and we want to collapse $\phi$ to a truth value of 1, then any consequences of $\phi$ had better be collapsed to 1 as well! In particular, if $$\| \psi \| = b$$, then $\psi$ should be collapsed to 1. If $\phi_1, \phi_2$ are collapsed to truth, we want $\phi_1 \land \phi_2$ to be collapsed to truth, so we require that $U$ be closed under $\land$. Additionally, exactly one of $\psi$ and $\lnot \psi$ should hold in the collapsed model, so exactly one of $a, \lnot a$ should be an element of $U$. 

Motivated by the above discussion, we can make precise definitions. A **filter** $F$ is a subset of $\mathbb{B}$ that is upward-closed and closed under joins (the first two points above). An **ultrafilter** $U$ is a filter such that for all $a \in \mathbb{B}$, exactly one of $a, \lnot a$ is an element of $U$. This definition of an ultrafilter is a special case of a [more general concept](https://en.wikipedia.org/wiki/Ultrafilter) with applications in topology. Happily, once we have decided to quotient $V^{\mathbb{B}}$ by an ultrafilter, there are no obstacles to the construction of a fully-fledged model of ZFC.

If $$\| x = y \| \in U$$, then we want $x=y$ to be true in the quotient model. Thus the objects of the model $V^{\mathbb{B}}/U$ should be equivalence classes $[x]$ of names of $V^{\mathbb{B}}$, with equivalence relation $$[x] \equiv [y] \Leftrightarrow \| x = y \| \in U$$. The relation $\in$ is defined on equivalence classes by $$[x] \in [y] \Leftrightarrow \| x \in y \| \in U$$. It is easily checked that this relation is well-defined on equivalence classes. 

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