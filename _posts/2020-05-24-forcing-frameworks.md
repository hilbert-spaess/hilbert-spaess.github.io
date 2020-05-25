---
title: Frameworks for forcing
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This post will hopefully serve to clarify the big-picture view of forcing, before I finally plunge into some juicy independence proofs. To recap, we've defined the [standard Boolean-valued model](https://hilbert-spaess.github.io/2020/05/16/Boolean-valued-semantics.html), and seen how to use this to [construct new ordinary models](https://hilbert-spaess.github.io/2020/05/23/building-actual-models.html) by quotienting by an ultrafilter. Of these, the more important is the forcing extension $V[G]$, a transitive extension of $V$ with many desirable properties. The generic ultrafilter $G$ satisfies two roles: it is the new set we add to our base model, and it is also the crucial 'truth filter' when collapsing a Boolean-valued model. At this point, a nasty meta-mathematical question pops up: if $V$ is **the** set-theoretic universe, then where does a new set $G$ come from?

## Countable models of ZFC

The simplest resolution of this problem is to assert that $V$ is decidedly not **the** set-theoretic universe in any Platonic sense. Indeed, we work in a bigger universe, and ensure that $V$ is fully understandable from our perspective.

We could ensure that $V$ is a countable model of ZFC. By the proof of the model existence lemma, any first-order language with countable constant symbols must have a countable model. It's also a theorem that any countable Boolean algebra has a generic ultrafilter. So from the outside, we can always locate a generic ultrafilter. In the case of say, constructing an extension in which CH is false, we will always be able to spot new real numbers (construed as generic filters on a particular Boolean algebra) from the outside.

This narrative is straightforward, but I find it mathematically and philosophically unsatisfying. It feels dirty to require degenerate models of ZFC to make this argument work. The approach I cover in the next section goes some way to rectifying this unpleasantness.

## Naturalistic conception of forcing

