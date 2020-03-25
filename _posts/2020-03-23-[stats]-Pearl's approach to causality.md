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

At this stage, we've noted that conditional independencies between variables under a distribution allow us to classify the Bayesian networks compatible with the distribution, and given a simple algorithmic criterion (d-separation) for looking up independencies of a distribution given a representative Bayesian network. Now we can start to talk about causality with a straight face, by introducing graphical causal models. We work in the context of a set of **observed variables**, with each variable a function of a subset of the other variables (with random peturbation).

**Definition:** A **causal structure** is a pair $(V, G)$, where $V = \{X_1, ..., X_n\}$ is a set of variables, and $G$ is a DAG with vertex-set $V$. Each edge of $G$ represents a functional relationship between vertices.

The causal structure specifies the underlying functional relationships. Given such a structure, a specific choice of functions will be termed a causal model:

**Definition:** A **causal model** on a causal structure $(V,G)$ is a specification of a function $x_i = f_i(pa_i, u_i)$ for each $X_i \in V$, where $PA_i$ is the parent-set of $X_i$, and the $u_i$ are independent vectors of uniform random variables.

The causal model now specifies a functional relationship between variables. The relevance of this definition of a causal model is predicated on three assumptions:
1. "Y is a (maybe non-deterministic) function of variables including X" is an adequate formalisation of "X exerts a causal influence on Y".
2. It suffices to consider 'Markovian' causal models (models such that the random disturbances 'u_i' are independent). This condition guarantees that there are no spurious dependencies between variables. This is a granularity assumption: we suppose that our model is detailed enough to capture all relevant variables, so that there are no unexplained correlations in observed data. It is obviously difficult to guarantee this a priori, so this is the assumption that we will violate later, when we consider semi-Markovian or 'latent' models.
3. It suffices to consider acyclic causal structures. This is another granularity assumption: our variables are sufficiently specific that there is no room for a cycle of causal dependencies.

**Definition:** Given a causal structure $(V, G)$ and a distribution $P$ on $V$, we say that $P$ is **consistent** with $G$ if there exists a choice of causal model on $(V,G)$ such that the entailed distribution is $P$. 

Let's work with an example (one of Pearl's favourites). Suppose there are three observable variables: the outcomes of two fair coin tosses, and the potential sounding of a gong. As observers, all we have is the joint distribution
 
(observation table)

## Latent Causal Models
