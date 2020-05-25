---
title: All quotients are extensions
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

[Having defined](https://hilbert-spaess.github.io/2020/05/23/building-actual-models.html) the forcing extension $V[G]$, it is possible to press on to a proof of the independence of CH from ZFC. This post is a brief detour from the main expository plotline. We show that even in the case that $U$ is not $V$-generic, the quotient model $V^{\mathbb{B}}/U$ has an interpretation as a forcing extension. Moreover, the way in which this is proved will be very instructive when we come to laying down a general meta-mathematical framework for forcing. The presentation and ideas here are mostly based on work by [Hamkins](https://arxiv.org/abs/1206.6075), although the proofs are slightly different.

## The base model in $V^{\mathbb{B}}/U$

Recall that each each set $x \in V$ has a canonical name $\breve{x} \in V^{\mathbb{B}}$. We define the name-class $\breve{V}$ via $$\| x \in \breve{V}\| = \bigvee_{y \in V}\| x = \breve{y}\|$$. Let $x_1, ..., x_n \in V$. Then it's a simple inductive proof to see that $$V \models \phi(x_1, ..., x_n) \Leftrightarrow \|\phi^{\breve{V}}(\breve{x_1}, ..., \breve{x_n})\| = 1$$. But we can construct $x \in V^{\mathbb{B}}$ such that $$\| x \in \breve{V}\| = 1$$, even though $x$ is not the canonical name of a set in $V$. If $\mathbb{B}$ is non-trivial, we can find a set of values $A \subseteq \mathbb{B}$  with disjunction 1, even though none of the values is itself 1. If, for example $$\| x = \breve{a} \| = a$$ for all $a \in A$, then $x$ is a sort of 'superposition' of canonical names, but is not itself a canonical name. For this reason, it is misleading to think of the predicate $\breve{V}$ as representing a class of canonical names. Let $$\hat{V} = \{x \in V^{\mathbb{B}}: \| x \in \breve{V}\| = 1\}$$. 

## The canonical name for a generic ultrafilter

The **canonical name for a generic ultrafilter** $\dot{G} \in V^{\mathbb{B}}$ was defined by $\mathcal{D}(\dot{G}) = \breve{\mathbb{B}}$, and for all $\breve{b} \in \mathbb{B}, \dot{G}(\breve{b}) = b$. We previously saw that if $G$ is any ultrafilter, then $\dot{G}^G = G$. More impressively, we will show that $V^{\mathbb{B}}$ believes $\dot{G}$ to be a $\breve{V}$-generic ultrafilter on $\breve{\mathbb{B}}$, in the sense that the statement that $\dot{G}$ is a generic ultrafilter has Boolean value 1. We will prove this in stages:

**$V^{\mathbb{B}}$ believes that $\breve{\mathbb{B}}$ is a Boolean algebra**: $$\| \breve{\mathbb{B}}$$ is a Boolean algebra $$\| = 1$$.

Denote by $\phi(B, \geq)$ the statement "$(B, \geq)$ is a Boolean algebra". Then since $\phi(B, \geq)$ is a $\Delta_0$ statement (it features only bounded quantification), we have $\phi^V(\breve{\mathbb{B}}, \breve{\geq}) = \phi(\breve{\mathbb{B}}, \breve{\geq})$, so by the work above, $$V \models \phi(\mathbb{B}, \geq) \Rightarrow \| \phi(\breve{\mathbb{B}}, \breve{\geq}) \| = 1$$.

**$$V^{\mathbb{B}}$$ believes $\dot{G}$ is an ultrafilter**: $$\| \dot{G}$$ is an ultrafilter on $$\breve{\mathbb{B}} \| = 1$$.

It's a straightfoward check that $$\| \dot{G} \subseteq \breve{\mathbb{B}} \| = 1$$.

$$\begin{align} \| x \in \dot{G} \land y \in \breve{\mathbb{B}} \land x \breve{\leq} y \| &= \bigvee_{b, c \in \mathbb{B}} \| x = \breve{b} \| \land G(\breve{b}) \land \| y = \breve{c} \|  \land \| x \breve{\leq} y \| \\ &\leq \bigvee_{b \leq c \in \mathbb{B}} \| x = \breve{b} \| \land b \land \| y = \breve{c} \| \\ &\leq \bigvee_{b \leq c \in \mathbb{B}} c \land \| y = \breve{c} \| \\ &= \| y \in \dot{G} \|  \end{align}$$

So $$\| \dot{G}$$ is upward-closed $$ \| = 1$$. A similar check shows that $\dot{G}$ is maximal and closed under intersections.

**$$V^{\mathbb{B}}$$ believes that $\dot{G}$ is a $\breve{V}$-generic ultrafilter**: $$\| \dot{G}$$ is $\breve{V}$-generic $$\| = 1$$. 

We use the dense-set characterisation of a generic ultrafilter. Suppose $S \subset \mathbb{B}$ is dense.

Then $$\| \dot{G} \cap \mathbb{B} \neq \emptyset \| = \bigvee_{b \in S}\|\breve{b} \in G \| = \bigvee_{b \in S} b = 1$$ (since $S$ is dense). 

## $V^{\mathbb{B}}/U$ is a forcing extension

We can now show that a quotient is itself a forcing extension with an exciting and important argument. The key idea is that because $V^{\mathbb{B}}$ believes it contains an inner model $\breve{V}$ of ZFC, a Boolean algebra $\breve{\mathbb{B}}$, and a $\breve{V}$-generic ultrafilter $\dot{G}$, we can actually talk about the forcing extension $\breve{V}[\dot{G}]$ inside $V^{\mathbb{B}}$. This argument will seem weird, and potentially confusing, but it's key to a view of forcing that Hamkins calls the "naturalistic conception". 

Important meta-mathematical viewpoint.

Believes it is a forcing extension. Names of names.

Deduce that general quotient is a forcing extension. 