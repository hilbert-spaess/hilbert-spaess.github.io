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

**Definition:** Given a causal structure $(V, G)$ and a distribution $P$ on $V$, we say that $P$ is **consistent** with $G$ if there exists a choice of causal model on $(V,G)$ such that the entailed distribution is $P$. Clearly if $P$ is consistent with $G$, $I(G) \subset I(P)$.  

## Minimality and Stability

The assumptions above are still not enough to identify the causal structure underlying an observed distribution. Let's work with an example. Suppose there are three observable variables: the outcomes of two coin tosses $C_1$ and $C_2$, and the potential sounding of a bell $B$. As observers, all we have is the joint distribution. The process underlying the variables is that the coins were tossed independently and fairly, and in the case that both landed heads-up, the gong was sounded.
 
(observation table) (correct structure)

Suppose we were trying to infer the correct model, given our above assumptions. By assumptions 2 and 3, the correct structure is a DAG on three variables. Since no variable is independent of the other two, the graph must be connected. No two variables are conditionally independent given the other, so the structure can't be one variable causing the other two, or a chain of two causations. So if the causal structure $G$ has two edges, they must be from $C_1$ and $C_2$ into $B$ (this is the correct structure). But there are models with three edges that are consistent with $P$ as well, as illustrated below. This is as far as we can get with the assumptions we've made so far.

(models with three edges)

Notice that one of the models shown above consists of the true two-edge structure with an additional causal link between $C_1$ and $C_2$. Pearl notes that by an Occam-like consideration, this structure is less preferable to the two-edge structure. In his typical combinatorial style, rather than introducing an Occam prior over causal networks, he instead puts a partial ordering on causal structures:

**Definition:** We say that causal structure $(V, G_1)$ **dominates** $(V, G_2)$ (written $G_1 > G_2$ ) if any causal model on $G_2$ can be simulated by a causal model on $G_1$. This domination is **strict** if $G_2$ does not dominate $G_1$. For example, $G$ dominates any subgraph. For a given distribution $P$, a causal structure $G$ is **minimal** with respect to $P$ if it is consistent with $P$, and does not strictly dominate any structure that is consistent with $P$. 

Now Pearl suggests that (in the spirit of selecting the most specific model) we should restrict our search to minimal structures with respect to $P$. This eliminates the example considered above. However, there are still minimal three-link structures we would like to exclude. These all feature a causal relation between $C_1$ and $C_2$. What we would like to do is reject these models on the grounds that $C_1$ and $C_2$ are observed to be marginally independent. Previously we rejected candidate causal structures on the grounds that independences in the structure should be reflected in the data. We would like to reverse this: any conditional independence observed in $P$ should be *explicable* by the structure $G$. This is the assumption of stability, or faithfulness:

**Definition:** A distribution $P$ is **stable** with respect to a causal structure $G$ if $I(P) = I(G)$. In other words, all conditional independencies in the observable data are explained by the independencies that we can read from $G$ using d-separation.

For any sensible measure over causal models on a given structure, almost all of the resulting distributions are stable with respect to the structure: you have to 'fine-tune' the parameters to generate conditional independencies that are not explicable by the structure. This is justification for the *assumption of stability*: the distribution under consideration is stable with respect to its causal structure. If $P$ satisfies this assumption, any minimal causal structure $G$ satisfies $I(G) = I(P)$, so all are d-separation equivalent. In our running example, there is a unique such structure. Although in this case we've identified the causal structure uniquely, this doesn't always happen. The best we can hope for is identification up to d-separation equivalence.

Inferred causation definition.

Yudkowsky uses a controversial example with the same uniquely identifiable three-variable causal structure as the coins-and-bell example above. He wants to investigate the causal relation between exercise and weight. He supposes that weight has a causal influence on exercise, but not vice-versa (you read that correctly), and that no other variable has an influence on both. We can't show this directly from the data, as this causal structure is d-separation equivalent to the same structure with the arrow reversed. However, we saw in the previous section that a 'V-shape' is identifiable from the data (assuming stability, minimality etc). So if we can find a third variable with an influence on exercise, and independent of weight, out pops the causal structure. Yudkowsky uses "Internet usage" as a candidate third variable. By looking at the distribution over weight, internet and exercise, we can infer the causal relation between weight and exercise! 

An interesting point raised in the comment section of Yudkowsky's piece highlights the relevance of the assumption of stability. The commenter writes that it *clearly can't be the case* that you could infer the causal influence of weight and internet usage on exercise. For suppose you had observed the same numbers, but with the weight variable replaced with hair colour. Then the same analysis would lead you to the absurd conclusion that hair colour has an influence on weight. But this is precisely the situation that the assumption of stability precludes- it's vanishingly unlikely that you'd see nubers that vindicate the V-structure unless there really is an underlying causal mechanism. You simply *wouldn't get* these numbers with a hair-colour variable.

## Latent Causal Models

The Markovian assumption is the least convincing of the assumptions we've made so far. It requires that the observer accept that there are no unobserved variables of causal import. For most questions of interest, this is an unhelpful assumption. There is a natural extension of the previous work to a setting that doesn't preclude models including latent variables. 

**Definition:** A **latent structure** is a pair $L = (G, O)$, where $D$ is a causal structure over $V$, and $O \subset V$ is a set of observed variables. That is, a latent structure is a substructure of a larger causal structure. The definitions of minimality and consistency extend to a latent structure. A distribution $P$ is stable with respect to the latent structure if all independencies among observed variables are consequences of the causal structure $G$.

projections.

Broadening the class of candidate models to all minimal latent models consistent with a given distribution, the previous definition of inferred causation applies. Excitingly, even expanding our search space in this fashion, there are still circumstances under which causal links can be inferred (ie, an arrow is present in every minimal latent model consistent with the  data). Let $R, D, M, C$ be four binary random variables: $R$ denotes whether a child's room is messy on a given day, $D$ denotes whether they ate their dinner, $M$ denotes whether their mother shouted, and $C$ denotes whether their mother cried. We have accumulated data for the joint distribution by observing these four variables over the past year. Suppose we observe that $R$ and $D$ are independent, that $C$ is independent of both $R$ and $D$ given $M$, and that there are no other independencies.

(pictures of some models of this)

The DAG must be connectec, as no variable is independent of the rest. The obvious model a) is consistent with the distribution, as is the less obvious model b). In both, note that there is a causal relation between $M$ and $C$. Reversing the arrow between $M$ and $C$ will break stability, as $R$ and $D$ will no longer be d-separated by the empty set. Similarly, postulating additional latent structure that explains $C$ and $M$ will break stability. So we can infer that the mother shouting causes the child to cry, purely from observational data.

Potential cause, genuine cause, spurious association.

## Identifying causal effect

The 'do' operation on causal networks. Relation to Rubin's action and potential outcome framework.

Definitions of causal effect using the 'do' operation.

Identifiability of causal effect. Examples.

## Summary and further questions

1. How do you extend a d-separation-duplicitous structure to a uniquely identifiable structure? What's the theory of d-separation equivalent DAGs.
2. Efficiently finding conditional independencies, and computing d-separation equivalence classes. Complexity classes of these problems.
3. Minimality vs priors etc. 
4. What if you don't have the full joint distribuion? Sampling bias stuff.
5. What does Pearl cite as good applications of his framework?
6. Where does conditional independence come in as the sole arbiter of consistency?
