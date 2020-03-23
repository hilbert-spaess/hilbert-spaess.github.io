<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is a summary of the start of Pearl's "Causality". Specifically, it covers the inference of causal relations in the absence of hidden variables.

## Bayesian networks and conditional independence 

Two quantities $X$ and $Y$ are independent if $P(X \vert Y) = P(X)$, so that the value of $Y$ tells us nothing about $X$, and vice versa. 

A Bayesian network is a suggestive shorthand for a joint probability density. Given a hierarchical Bayesian model, the joint density can often be factored into conidion
