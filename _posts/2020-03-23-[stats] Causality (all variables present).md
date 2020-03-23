

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is a summary of the start of Pearl's "Causality". Specifically, it covers the inference of causal relations in the absence of hidden variables.

## Bayesian networks and conditional independence 

Two quantities $x$ and $y$ are independent if $P(x \vert y) = P(x)$, so that the value of $y$ tells us nothing about $x$, and vice versa. A generalisation of this concept is the notion of **conditional independence**: $x$ and $y$ are conditionally independent, given $z$, if $P(x \vert y, z) = P(x,z)$. We write this as $$(x \perp y | z)\_P$$. 

A Bayesian network is a suggestive shorthand for a joint probability density. Given a hierarchical Bayesian model, the joint density can often be factored into conidion
