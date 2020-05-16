<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is the first post in a projected multi-post sequence on *forcing* and its use in independence proofs in set theory. I'm hoping to take the sequence in a philosophical direction, but this is an area of philosophy for which quite a lot of (thankfully attractive) maths is needed. The intended pre-requisites are an understanding of first-order logic up to the completeness theorem. [Written by a beginner etc].

## What is a model?

A model is a structure with which we can interpret sentences in a formal language. Loosely, by interpretation we mean assigning a truth value to the sentence according to whether it holds in the model. In the familiar first-order language of sets, an example of a *sentence* $\phi$ is $(\exists y)(\forall x)(x \not \in y)$. An example of a model of the language of sets might be $M$ = \{ \{1\}, \{1,2\} \}, interpreting the formal $\in$ relation as standard set inclusion. By inspection, $\phi$ is true according to its obvious M-interpretation. 

Let's recall the inductive definition of M-interpretation $\phi_M$ of a sentence $\phi$, for an arbitrary first-order language $L$, with function constants $\Omega$ and relation constants $\Pi$. Functions $f \in \Omega$ and relations $r \in \Pi$ have interpretations as function and relation $f_A$ and $r_A$ on $M$ as a set. [Define atomic formulae]. [Define truth values of full sentences by inspection on the model.]

[Assigning truth values to atomic formulae, then extrapolating].

[Multi-valued notion of truth. Need corresponding and, or, and not. The correct structure here is a Boolean algebra.

## Boolean-valued models of propositional logic

We start with the simpler language of propositional logic. This consists of a family of *primitive propositions* $P$, represented by symbols like $p,q,r$, which are the atomic formulae. Sentences consist of these atomic formulae assembled with the usual logical connectives of $\land, \lor, \lnot$, and $\Rightarrow$.  [Models of propositional logic, aka valuations].

[Boolean-valued models of proposition logic, and an application].

## The standard Boolean-valued model of set theory

## Quotienting by a filter

## Building V[G]