---
title: Frameworks for forcing
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This post will hopefully serve to clarify the big-picture view of forcing, before I finally plunge into some juicy independence proofs. To recap, we've defined the [standard Boolean-valued model](https://hilbert-spaess.github.io/2020/05/16/Boolean-valued-semantics.html), and seen how to use this to [construct new ordinary models](https://hilbert-spaess.github.io/2020/05/23/building-actual-models.html) by quotienting by an ultrafilter. Of these, the more important is the forcing extension $V[G]$, a transitive extension of $V$ with many desirable properties. The generic ultrafilter $G$ satisfies two roles: it is the new set we add to our base model, and it is also the crucial 'truth filter' when collapsing a Boolean-valued model. At this point, a nasty meta-mathematical question pops up: if $V$ is **the** set-theoretic universe, then where does a new set $G$ come from?

## Countable models of ZFC

The simplest resolution of this problem is to assert that $V$ is decidedly not **the** set-theoretic universe in any Platonic sense. Indeed, we work in a bigger universe, and ensure that $V$ is fully understandable from our perspective.

We could ensure that $V$ is a countable model of ZFC. By the proof of the model existence lemma, any first-order language with countable constant symbols must have a countable model. It's also a theorem that any countable Boolean algebra has a generic ultrafilter. So from the outside, if we assert that $V$ is countable,  we can always locate a generic ultrafilter with which to extend. In the case of say, constructing an extension in which CH is false, we will always be able to spot new real numbers (construed as generic filters on a particular Boolean algebra) from the outside.

This narrative is straightforward, but I find it mathematically and philosophically unsatisfying. It feels dirty to require degenerate models of ZFC to make this argument work. The approach I cover in the next section goes some way to rectifying this unpleasantness.

## Naturalist account of forcing

I was happy to come across a paper by Joel Hamkins entitled ["The Set-theoretic Multiverse"](https://arxiv.org/abs/1108.4223). The author seems to have a similar aversion to restricting the possibility of constructing a forcing extension to only "degenerate models" like countable models. He succinctly presents an account of forcing that legitimises behaving as if, given a universe $V$, and a complete Boolean algebra $\mathbb{B} \in V$, you can pluck a generic ultrafilter out of a hat and move to working in $V[G]$. This rests on our previous work showing that the standard Boolean-valued model [believes it contains a generic ultrafilter](https://hilbert-spaess.github.io/2020/05/24/All-quotients-are-extensions.html). Hamkins' approach is replicated below, for completeness of these notes, but if you've read this far I recommend you check out the paper and get it from the horse's mouth. 

**Naturalist account of forcing:** If $V$ is a universe of set theory, and $\mathbb{B}$ a complete Boolean algebra, then $V^{\mathbb{B}}/U$ is in $V$ a definable class model of the theory that axiomatises what it means to be a forcing extension of $V$. In particular, this class models the following theory in the first-order language containing $\in$, a predicate for $V$, a constant symbol $G$, and constant symbols for every element of $V$:
(1) Every sentence that holds in $V$ (with explicit references to elements of $V$ using the constant-symbols available), relativised to the predicate for $V$. (In particular, the axioms of ZFC relativised to $V$).
(2) The claim that $V$ is a transitive proper class.
(3) The claim that $G$ is a $V$-generic ultrafilter on $\mathbb{B}$.
(4) The claim that the universe is $V[G]$, and is a model of ZFC.

All of this follows from the properties of $V^{\mathbb{B}}/U$ that we derived. The interpretation of the predicate for $V$ is as $\breve{V}_U$. The constant symbols for elements of $V$ are interpreted as $[\breve{x}]_U$, and $G$ is interpreted as $[\dot{G}]_U$. 


