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

If $$\| x = y \| \in U$$, then we want $x=y$ to be true in the quotient model. Thus we define the objects of the model $V^{\mathbb{B}}/U$ as equivalence classes $[x]$ of names of $V^{\mathbb{B}}$:

$$[x] \equiv_U [y] \Leftrightarrow \| x = y \| \in U$$  
$$[x] \in_U [y] \Leftrightarrow \| x \in y \| \in U$$

It is easily checked that the relation $\in$ is well-defined on equivalence classes. Thus $(V^{\mathbb{B}}/U, \in_U)$ is a model of the language of set theory.

## $V^{\mathbb{B}}/U \models$ ZFC

Recall that $V^{\mathbb{B}}$ is a **full** BVM: for every $\phi(x, y)$, there is some $a \in V^{\mathbb{B}}$ such that $$\| (\exists x) \phi(x,y) \| = \| \phi(a, y) \|$$. This is an important fact for the following theorem:

**Los' theorem:** $$V^{\mathbb{B}} \models \phi([x_1], ... [x_n]) \Leftrightarrow \| \phi(x_1, ..., x_n) \| \in U$$.

The proof is by induction on the complexity of $\phi$.

Crucially, every axiom of ZFC is valid in $V^{\mathbb{B}}$, so holds in $V^{\mathbb{B}}/U$. Note that we don't really have a good picture of what $V^{\mathbb{B}}/U$ looks like in comparison to $V$. It was constructed in a roundabout manner with equivalence classes. When combined with Los' theorem, our [previous work](https://hilbert-spaess.github.io/2020/05/22/$V-B$-models-ZFC.html) tells us that the map $x \to [\dot{x}]$ is an embedding of $V$ in $V^{\mathbb{B}}/U$. So there's at least as much stuff in the new quotient model.

Thus far, it might have been tacitly assumed that $U \in V$. However, in this case it turns out that we haven't made anything new at all. For any name $x$, the set $$x' = \{y \in x : x(y) \in U\} \in V$$, so $$\| x = x^{*}\| \in U$$, and $[x] = [x']$. So the map between $V$ and $V^{\mathbb{B}}/U$ is in fact an isomorphism of models. In order for this construction to be interesting, $U$ has to come from *outside* the universe of sets we are working with. If this sounds crazy, you can assume for now that $V$ is some neutered model of ZFC, so that there are plenty of ultrafilters kicking around that $V$ doesn't have access to. If $V$ is 'our' universe of set theory, I'll try and make sense of the relevant metamathematics in a later post.

## The extension $V[G]$

Suppose we've selected an ultrafilter $G$ (for reasons that will be clear later, we use an alternative letter to denote an ultrafilter in this section). Rather than indirectly constructing the elements of a model by defining equivalence classes as above, we could attempt to concretely interpret the names of $V^{\mathbb{B}}$ as subsets of $V$. For a name $x$, and $y \in \mathcal{D}(x)$, we would like to keep $y$ as a genuine member of $x$ if $x(y) \in U$, and forget about $y$ otherwise. Of course, $y$ itself is a name, so we'd want to apply the same construction all the way down. This motivates a precise recursive definition of the **interpretation** $x^G$ of a name $x \in V^{\mathbb{B}}$ by an ultrafilter $G$:

$$ \emptyset^G = \emptyset $$  
$$ x^G = \{ y^G : x(y) \in G \}$$.

The class $$V[G] = \{ x^G : x \in V^{\mathbb{B}} \}$$ is a new candidate model of ZFC. This is the **forcing extension** of $V$ by $G$. Note the contrast with the quotient model: the emphasis on this construction of the forcing extension is the interpretability of the objects. Again, the construction is only interesting if $G \not \in V$, and my meta-mathematical recommendation is to assume that we are working in a larger set-theoretic universe than $V$, and are privy to ultrafilters such as $G$ to which $V$ doesn't have access.

It's an easy proof by induction that $\dot{x}^G = x$, so $V \subset V[G]$. It's also an easy check that $\dot{G}^G = G$, so $G \in V[G]$. Finally, note that if $M$ is a model of ZFC with $V \subset M, G \in M$, then the construction of $V^G$ can be carried out in $M$, so that $V[G] \subset M$. These facts got some way to justfiying the suggestive extension notation. 

Ideally, it would turn out that $V^{\mathbb{B}}/G$ and $V[G]$ are isomorphic. This is almost the case, and it holds with one more condition on $G$. We require that $G$ be closed the joins of arbitrary $V$-subsets. In this case we call $G$ a **V-generic ultrafilter**. This extra property is precisely what is needed to show the following:

**Equivalence of generic quotient and extension:** If $G$ is $V$-generic, then $V[G]$ is isomorphic to $V^{\mathbb{B}}/G$. In particular, it follows that $$V[G] \models \phi(x_1^G, ..., x_n^G) \Leftrightarrow \| \phi(x_1, ..., x_n) \| \in G$$, and hence $V[G]$ is a model of ZFC.

It suffices to show that

$$x^G = y^G \Leftrightarrow \| x = y \| \in G$$  
$$x^G \in y^G \Leftrightarrow \| x \in y \| \in G$$

We carry out a simultaneous proof by induction. 

Generic model theorem is a rephrasing of the above. 

## Arbitrary quotient as extension

What breaks with the isomorphism when non-generic?

Quotient as a forcing extension of a different base model.

## What of genericity?

The two roles: new set being added, and filter on truth. This is witchcraft and I really don't understand it. Will try and understand it.

So far, the reason we wanted a generic ultrafilter was to make the extension-as-quotient argument work. Is there a way of motivating it as a 'typical set?'. Something tantalasing I noticed: when adjoining a Cohen generic real, the generic real must be normal.