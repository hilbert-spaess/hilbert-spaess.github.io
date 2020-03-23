---
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is a summary of the start of Pearl's "Causality". Specifically, it covers the inference of causal relations in the absence of hidden variables.

## Bayesian networks and conditional independence 

Two variables $x$ and $y$ are independent if $P(x \vert y) = P(x)$, so that the value of $y$ tells us nothing about $x$, and vice versa. A generalisation of this concept is the notion of **conditional independence**. Given a finite set of variables $V$, and three subsets $X, Y, Z \subset V$, we say that $X$ and $Y$ are conditionally independent, given $Z$, if $P(X \vert Y, Z) = P(X, Z)$. We write this as $$(X \perp_P Y \vert Z)$$. An intuition to have here is that Z "screens off" $X$ from $Y$.

A Bayesian network is a suggestive shorthand for a joint probability density. If there is a hierarchy of dependencies among the variables involved, then the joint density can be written as a product of conditional densities. For example, in the survival curve model I've previously discussed, there's a factorisation $P(J, k, m, x) = P(J)P(k|J)P(m|J)P(x|k,m)$. This has a clear representation as a directed acyclic graph (DAG), with an arrow from $x$ to $y$ if $x$ features in the conditional density of $y$. 

(picture here)

In general, given a joint density $P$ over an ordered set of variables $X_1, ..., X_n$, we can decompose it as $\prod_{i=1}^n P(x_i \vert x_1, ..., x_{i-1})$. For a minimal set $pa_i$ of predecessors of $x_i$, we term

## d-separation


