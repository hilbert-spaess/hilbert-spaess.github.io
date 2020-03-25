---
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

I've been reading some of Pearl's "Causality". Specifically, I've been looking at his take on inferring causal structure from raw experimental data. The canonical problem here is to infer the causal relationships between observable variables, given only their joint distribution. This problem is often insoluble without making assumptions on the models we consider. For example, there are lots of causal structures that explain two correlated variables A and B. A could 'cause' B, B could 'cause' A, or there could be an unobserved variable C that causally influences both. Pearl's contribution appears to be to provide clear conditions under which we can make precise statements about the underlying causal structure of a distribution.

Pearl makes frequent use of graphical models- indeed, he was one of their first proponents in the service of simplifying inference. Everything of his that I've read has an algorithmic flavour, and reads more like graph theory than statistics. That said, I'm unsure about how his methods hold up in applications against, for example, the approach to causality in Gelman's "Bayesian Data Analysis".

## Preliminaries: Bayesian networks and conditional independence 

Two variables $x$ and $y$ are independent if $P(x \vert y) = P(x)$, so that the value of $y$ tells us nothing about $x$, and vice versa. A generalisation of this concept is the notion of **conditional independence**. Given a finite set of variables $V$, and three subsets $X, Y, Z \subset V$, we say that $X$ and $Y$ are conditionally independent, given $Z$, if $P(X \vert Y, Z) = P(X, Z)$. We write this as $$(X \perp_P Y \vert Z)$$. An intuition to have here is that Z "screens off" $X$ from $Y$.

A Bayesian network is a suggestive shorthand for a joint probability density. If there is a hierarchy of dependencies among the variables involved, then the joint density can be written as a product of conditional densities. For example, in the survival curve model I've previously discussed, there's a factorisation $P(J, k, m, x) = P(J)P(k\vert J)P(m\vert J)P(x\vert k,m)$. This has a clear representation as a directed acyclic graph (DAG), with an arrow from $x$ to $y$ if $x$ features in the conditional density of $y$. 

(picture here)

In general, given a joint density $P$ over an ordered set of variables $X_1, ..., X_n$, we can decompose it as $\prod_{i=1}^n P(x_i \vert x_1, ..., x_{i-1})$. We term a minimal set $pa_i$ of predecessors of $x_i$ a set of **Markovian parents** of $x_i$. We say that the distribution $P$ is **represented** by a DAG $G$ if there is an ordering of the vertices of $G$ such that directed edges correspond precisely to Markovian parenthood. In the survival curve example above, we have represented the joint density by a three-tiered DAG. $J$ is the sole Markovian parent of $m,k$, and the set of Markovian parents of $x$ is $\{m,k\}$. Note that the model admits functional interpretations of these arrows. To a human eye, the diagram both simplifies the task of computing the density, and suggests an explanation for dependencies among the variables.

Key idea: we get probabilistic data. Humans expect observed indepencies to *have an explanation*: ie to be engendered by a causal graphical model.

## Preliminaries 2: d-separation

## Causal models

At this stage, we've noted that conditional independencies between variables allow us to construct compatible graphical models. Most examples of graphical models for probability distributions

**Definition:** 

Key idea: we get probabilistic data. Humans expect observed indepencies to *have an explanation*: ie to be engendered by a causal graphical model.

