---
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

I've been reading some of Pearl's "Causality". Specifically, I've been looking at his take on inferring causal structure from raw experimental data. The canonical problem here is to infer the causal relationships between observable variables, given only their joint distribution. This problem is often insoluble without making assumptions on the models we consider. For example, there are lots of causal structures that explain two correlated variables A and B. A could influence B, B could influence A, or there could be an unobserved variable C that causally influences both. Pearl's contribution appears to be to provide clear conditions under which we can make statements about the underlying causal structure of a distribution.

Pearl makes frequent use of graphical models- indeed, he was one of their first proponents in the service of simplifying inference. Everything of his that I've read has an algorithmic flavour, and reads more like graph theory than statistics. That said, I'm unsure about how his methods hold up in applications against, for example, the approach to causality in Gelman's "Bayesian Data Analysis".

## Preliminaries: Bayesian networks and conditional independence 

Two variables $x$ and $y$ are independent if $P(x \vert y) = P(x)$, so that the value of $y$ tells us nothing about $x$, and vice versa. A generalisation of this concept is the notion of **conditional independence**. Given a finite set of variables $V$, and three subsets $X, Y, Z \subset V$, we say that $X$ and $Y$ are conditionally independent, given $Z$, if $P(X \vert Y, Z) = P(X, Z)$. We write this as $$(X \perp_P Y \vert Z)$$. An intuition to have here is that Z "screens off" $X$ from $Y$.

A Bayesian network is a suggestive shorthand for a joint probability distribution. If there is a hierarchy of dependencies among the variables involved, then the joint density can be written as a product of conditional densities. For example, in a survival curve model I've [previously used](https://hilbert-spaess.github.io/STATS-survival-curves/), there's a factorisation $P(J, k, m, x) = P(J)P(k\vert J)P(m\vert J)P(x\vert k,m)$. This has a clear representation as a directed acyclic graph (DAG), with an arrow from $x$ to $y$ if $x$ features in the conditional density of $y$. 

![DAG example](/images/dag_example.jpg){:class="img-responsive"}

In general, given a joint density $P$ over an ordered set of variables $X_1, ..., X_n$, we can decompose it as $\prod_{i=1}^n P(x_i \vert x_1, ..., x_{i-1})$. We use this notation for the following definitions:

**Definition:** A set of **Markovian parents** of $x_i$ is a minimal set $pa_i$ of predecessors of $x_i$ such that $P(x_i \vert x_1, ..., x_{i-1}) = P(x_i \vert pa_i)$.

**Definition:** The distribution $P$ is **represented** by a DAG $G$ if there is a bijection between the vertices of $G$ and $X_1, ..., X_n$ such that the predecessors of each vertex are a set of Markovian parents.

To a human eye, this representation is more useful than a grid of probabilities. We'd expect it to be easier to read off information like conditional independence with this representation. Indeed, it turns out that there is a simple visual criterion, known as d-separation.

## Preliminaries: d-separation

Here are DAG representations for three simple three-variable distributions:

![Three DAGs](/images/three_dags.jpg)

Lets call these a "chain", a "wedge", and a "vee". For a long path of edges, any pair of consecutive edges come together to form one of these three structures. For the first two, any two of the three variables are marginally dependent. In the chain, we have $C \perp A \vert B$. In other words, finding out about $B$ means that $A$ no longer tells you anything about $C$. This follows precisely from the Markovian observation (to get better intuition, you can think causally, even though we haven't mentioned causation yet!) Similarly, in the wedge, no two variables are independent, but $E \perp F \vert D$. The vee is slightly different: $G$ and $H$ are marginally independent, but conditioning on $I$ might render them dependent. 

These three dependence structures will actually be enough to give a criterion for ascertaining all conditional independencies that follow from the structure of a graph! We'll look for one of the 'three reasons' above that conditioning on one variable might make another two independent.

**Definition:** Let $x$ and $y$ be vertices of a DAG $G$, and let $Z$ be a subset of the vertex-set. A path between $x$ and $y$ is any chain of edges (ignoring direction) that starts at $x$ and ends at $y$. A path is **d-separated** by $Z$ if it contains a chain or a wedge with central vertex in $Z$, or it contains a vee with central vertex and all descendants thereof not in $Z$. We say that $x$ and $y$ are **d-separated in G** if any path between them is d-separated by $Z$. We say sets of vertices $X$ and $Y$ are d-separated if any $x \in X, y \in Y$ are d-separated.

**Theorem:** If $X$ and $Y$ are d-separated by $Z$ in $G$, for any distribution $P$ represented by $G$, $(X \perp_P Y) \vert Z$. Conversely, if $X$ and $Y$ are not d-separated, then for almost all distributions represented by $G$, $X$ and $Y$ are conditionally dependent given $Z$.

So the independences that are 'forced to hold' by the structure can be read off using the criterion of d-separation. Furthermore, for almost all compatible distributions, these are precisely the independences that occur.

**Definition:** For a distribution $P$, we write $I(P)$ for the set of conditional independencies observed in $P$. For a DAG $G$ we write $I(G)$ for the set of d-separation statements entailed by $G$. The theorem above states that if $P$ is represented by $G$, then $I(G) \subset I(P)$, and for almost all such $P$, $I(G) = I(P)$. 

Note that a graph such that $I(G) = I(P)$ is definitely not unique up to graph isomorphism. So there is not a unique graph structure compatible with a given distribution. This will be important as we move on to causality.

**Theorem:** Given a labelling of the vertices of $G$, if $I(G) \subset I(P)$, then $P$ is represented by $G$. (This follows immediately from the fact that vertices are d-separated from non-descendants by their predecessors, so the predecessors are indeed Markov parents).

## Causal models

At this stage, we've noted that conditional independencies between variables under a distribution allow us to classify the Bayesian networks compatible with the distribution, and given a simple algorithmic criterion (d-separation) for looking up independencies of a distribution given a representative Bayesian network. 

Now we note that DAGs have a natural causal interpretation, translating a directed edge with the phrase "has an influence on". A causal structure will be a DAG with randoma variables as vertices, and arrows indicating a direction functional link.

**Definition:** A **causal structure** is a pair $(V, G)$, where $V = \{X_1, ..., X_n\}$ is a set of variables, and $G$ is a DAG with vertex-set $V$. Each edge of $G$ represents a functional relationship between vertices.

The causal structure specifies the underlying functional relationships. Given such a structure, a specific choice of (non-deterministic) functions will be termed a causal model:

**Definition:** A **causal model** on a causal structure $(V,G)$ is a specification of a function $x_i = f_i(pa_i, u_i)$ for each $X_i \in V$, where $PA_i$ is the parent-set of $X_i$, and the $u_i$ are independent vectors of uniform random variables.

The causal model now specifies a functional relationship between variables. The relevance of this definition of a causal model is predicated on three assumptions:
1. "Y is a (maybe non-deterministic) function of variables including X" is an adequate formalisation of "X exerts a causal influence on Y".
2. It suffices to consider 'Markovian' causal models (models such that the random disturbances $u_i$ are independent). For such models, the induced distribution is represented by its causal structure as a Bayesian network. This condition guarantees that there are no spurious dependencies between variables. This is a granularity assumption: we suppose that our model is detailed enough to capture all relevant variables, so that there are no unexplained correlations in observed data. It is obviously difficult to guarantee this a priori, so this is the assumption that we will violate later, when we consider semi-Markovian or 'latent' models.
3. It suffices to consider acyclic causal structures. This is another granularity assumption: our variables are sufficiently specific that there is no room for a cycle of causal dependencies.

**Definition:** Given a causal structure $(V, G)$ and a distribution $P$ on $V$, we say that $P$ is **consistent** with $G$ if there exists a choice of causal model on $(V,G)$ such that the entailed distribution is $P$. Clearly if $P$ is consistent with $G$, $I(G) \subset I(P)$. The converse holds, as above.

## Minimality and Stability

The assumptions above are still not enough to identify the causal structure underlying an observed distribution. Let's work with an example. Suppose there are three observable variables: the outcomes of two coin tosses $C_1$ and $C_2$, and the potential sounding of a bell $B$. As observers, all we have is the joint distribution. The process underlying the variables is that the coins were tossed independently and fairly, and in the case that both landed heads-up, the gong was sounded.
 
| $C_1$| $C_2$ | B | Probability
| H | H | 0 | 0
| H | H | 1 | 1/4
| H | T | 0 | 1/4
| H | T | 1 | 0
| T | H | 0 | 1/4
| T | H | 1 | 0
| T | T | 0 | 1/4
| T | T | 1 | 0

![coin true](/images/coin_true.jpg)

Suppose we were trying to infer the correct model, given our above assumptions. By assumptions 2 and 3, the correct structure is a DAG on three variables. Since no variable is independent of the other two, the graph must be connected. No two variables are conditionally independent given the other, so the structure can't be one variable causing the other two, or a chain of two causations. So if the causal structure $G$ has two edges, they must be from $C_1$ and $C_2$ into $B$ (this is the correct structure). But there are models with three edges that are consistent with $P$ as well, as illustrated below. This is as far as we can get with the assumptions we've made so far.

![coin extra](/images/coin_extra.jpg) | ![coin unstable](/images/coin_unstable.jpg)

Notice that above left-hand model consists of the true two-edge structure with an additional causal link between $C_1$ and $C_2$. Pearl notes that by an Occam-like consideration, this structure is less preferable to the two-edge structure. In his typical combinatorial style, rather than introducing an Occam prior over causal networks, he instead puts a partial ordering on causal structures:

**Definition:** We say that causal structure $(V, G_1)$ **dominates** $(V, G_2)$ (written $G_1 > G_2$ ) if any causal model on $G_2$ can be simulated by a causal model on $G_1$. This domination is **strict** if $G_2$ does not dominate $G_1$. For example, $G$ dominates any subgraph. For a given distribution $P$, a causal structure $G$ is **minimal** with respect to $P$ if it is consistent with $P$, and does not strictly dominate any structure that is consistent with $P$. 

Now Pearl suggests that (in the spirit of selecting the most specific model) we should restrict our search to minimal structures with respect to $P$. This eliminates the example considered above. However, there are still minimal three-link structures we would like to exclude, like the above-right example These all feature a causal relation between $C_1$ and $C_2$. What we would like to do is reject these models on the grounds that $C_1$ and $C_2$ are observed to be marginally independent. Previously we rejected candidate causal structures on the grounds that independences in the structure should be reflected in the data. We would like to reverse this: any conditional independence observed in $P$ should be *explicable* by the structure $G$. This is the assumption of stability, or faithfulness:

**Definition:** A distribution $P$ is **stable** with respect to a causal structure $G$ if $I(P) = I(G)$. In other words, all conditional independencies in the observable data are explained by the independencies that we can read from $G$ using d-separation.

For any sensible measure over causal models on a given structure, almost all of the resulting distributions are stable with respect to the structure: you have to 'fine-tune' the parameters to generate conditional independencies that are not explicable by the structure. This is justification for the *assumption of stability*: the distribution under consideration is stable with respect to its causal structure. If $P$ satisfies this assumption, any minimal causal structure $G$ satisfies $I(G) = I(P)$, so all are d-separation equivalent. In our running example, there is a unique such structure. Although in this case we've identified the causal structure uniquely, this doesn't always happen. The best we can hope for is identification up to d-separation equivalence.

Yudkowsky uses a [controversial example](https://www.lesswrong.com/posts/hzuSDMx7pd2uxFc5w/causal-diagrams-and-causal-models) with the same uniquely identifiable three-variable causal structure as the coins-and-bell example above. He wants to investigate the causal relation between exercise and weight. He supposes that weight has a causal influence on exercise, but not vice-versa (you read that correctly), and that no other variable has an influence on both. We can't show this directly from the data, as this causal structure is d-separation equivalent to the same structure with the arrow reversed. However, we saw in the previous section that a 'V-shape' is identifiable from the data (assuming stability, minimality etc). So if we can find a third variable with an influence on exercise, and independent of weight, out pops the causal structure. Yudkowsky uses "Internet usage" as a candidate third variable. By looking at the distribution over weight, internet and exercise, we can infer the causal relation between weight and exercise! 

An interesting point raised in the comment section of Yudkowsky's piece highlights the relevance of the assumption of stability. The commenter writes that it *clearly can't be the case* that you could infer the causal influence of weight and internet usage on exercise. For suppose you had observed the same numbers, but with the weight variable replaced with hair colour. Then the same analysis would lead you to the absurd conclusion that hair colour has an influence on weight. But this is precisely the situation that the assumption of stability precludes- it's vanishingly unlikely that you'd see nubers that vindicate the V-structure unless there really is an underlying causal mechanism. You simply *wouldn't get* these numbers with a hair-colour variable.

## Latent Causal Models

The Markovian assumption is the least convincing of the assumptions we've made so far. It requires that the observer accept that there are no unobserved variables of causal import. For most questions of interest, this is an unhelpful assumption. There is a natural extension of the previous work to a setting that doesn't preclude models including latent variables. 

**Definition:** A **latent structure** is a pair $L = (G, O)$, where $D$ is a causal structure over $V$, and $O \subset V$ is a set of observed variables. That is, a latent structure is a substructure of a larger causal structure. The definitions of minimality and consistency extend to a latent structure. A distribution $P$ is stable with respect to the latent structure if all independencies among observed variables are consequences of the causal structure $G$.

(projections).

Broadening the class of candidate models to all minimal latent models consistent with a given distribution, the previous definition of inferred causation applies. Excitingly, even expanding our search space in this fashion, there are still circumstances under which causal links can be inferred (ie, an arrow is present in every minimal latent model consistent with the  data). Let $R, D, M, C$ be four binary random variables: $R$ denotes whether a child's room is messy on a given day, $D$ denotes whether they ate their dinner, $M$ denotes whether their mother shouted, and $C$ denotes whether their mother cried. We have accumulated data for the joint distribution by observing these four variables over the past year. Suppose we observe that $R$ and $D$ are independent, that $C$ is independent of both $R$ and $D$ given $M$, and that there are no other independencies.

(pictures of some models of this)

The DAG must be connectec, as no variable is independent of the rest. The obvious model a) is consistent with the distribution, as is the less obvious model b). In both, note that there is a causal relation between $M$ and $C$. Reversing the arrow between $M$ and $C$ will break stability, as $R$ and $D$ will no longer be d-separated by the empty set. Similarly, postulating additional latent structure that explains $C$ and $M$ will break stability. So we can infer that the mother shouting causes the child to cry, purely from observational data.

## Criteria for inferrability of causal relations

A common thread in previous examples is that inferring causal relation between $X$ and $Y$ required the introduction of auxiliary variables, and observation of particular patterns of dependency among these variables. Pearl notes that this shouldn't be that surprising, as the core of causal claims concerns the behaviour of $X$ and $Y$ in relation to a variable $Z$ that corresponds to external manipulation of $X$ or $Y$. The methodology of observational causal inference is to choose a variable $Z$ among the observed data to act as a 'virtual manipulator', as if 'nature had performed the experiment itself'.

Suppose we have an observed distribution $P$ (stable w.r.t its causal structure) on observed variables $O$, and are attempting to infer the causal relation between $X$ and $Y$. We say that $X$ has a **genuine causal influence** on $Y$ if there is a directed edge between $X$ and $Y$ in all minimal structures compatible with the distribution. We say that $X$ has a **potential causal influence** on $Y$ if, in every compatible structure, there is either a directed path $X$ to $Y$ or there is a latent common cause. We say there is a **spurious association** between the variables if for every minimal structure there is a latent common cause. Otherwise there is an **undetermined relationship** between $X$ and $Y$. It turns out that there are simple local criteria for ascertaining these relationships.

**Claim:** $X$ has a potential causal influence on $Y$ iff:
1. $X$ and $Y$ are dependent in every context (ie given that a set of variables is tied to specific values).
2. There exists a variable $Z$ and a context $S$ such that $X \perp Z \vert S$ and $Z \not \perp Y \vert S$.

**Proof:** The if component is fairly straightforward. The fact that $X$ and $Y$ are dependent in every context implies that there exists a path between the two that is not d-separated by the rest of the variables. This is either a direct edge or a latent cause. The second condition precludes an arrow from $Y$ to $X$. The only-if part is a combinatorics problem about edge-flipping.

**Claim:** A variable $X$ has a genuine causal influence on $Y$ iff there exists a variable $Z$ such that:
1. $X$ and $Y$ are dependent in any context and there exists a context $S$ such that: $Z$ is a potential cause of $X$, $Z$ and $Y$ are dependent given $S$, and $Z$ and $Y$ are independent given $S \cup X$.

**Proof:** If component is easy again. Only-if component another combinatorics problem.

**Claim:** Variables $X$ and $Y$ are spuriously associated iff they are dependent in every context and there exist two variables $Z_1, Z_2$ and two contexts $S_1, S_2$ that disqualify $X$ as a cause of $Y$ and $Y$ as a cause of $X$, as in the first claim.

So checking for an inferrable genuine causal relation is as simple as looking for a third variable $Z$ with the desired independence properties. In the example of the mother and child above, $C$ shows that $R$ is a potential cause of $M$. Then $R$ shows that $M$ is a genuine cause of $C$. It is not possible to find a third variable to demonstrate that $R$ is a genuine cause of $M$, showing that there exist structures in which $R$ and $M$ have a common latent cause.

## Identifying causal effect

Distributions and causal structures are useful for answering different questions. With the observable distribution, we can answer questions like, "Given that the child's room is messy, what is the probability that the child cries today?" With a causal structure, we can answer questions like "What happens if I mess up the child's room?". To see the difference, note that if messiness of room and angriness of mother were explicable by a latent common cause, we wouldn't expect messing up the room to affect the chances of shouting and crying later on. If messiness of room was indeed a cause of angriness of mother, we would expect to see such a difference. Structureless distributions give us information about *association*, and structures allow us to consider the outcomes of *intervention*.

To understand the consequences of intervention, Pearl introduces the 'do' operation. Let $P$ a distribution induced by a causal model with structure $G$, and let $X$ and $Y$ be two sets of observed variables. The probability conditioned on setting $Y$ to $y$ is denoted $P(X \vert Y = y)$.

**Definition:** The **causal effect** of $Y$ on $X$, or the **distribution after intervention Y = y**, is written $P(X \vert \hat{y})$. For each realisation $y$ of $Y$, it gives the distribution induced by deleting all equations in the causal model corresponding to variables of $Y$, and substituting $Y = y$ in the remaining equations. This corresponds to restricting the causal model to the substructure formed by deleting all edges into $Y$.

Suppose we want to compute the causal effect of smoking on lung cancer. As usual, we can't infer anything about causation from just a distribution over smoking and cancer (some tobacco companies maintain that the relationship is due to a latent common cause, rather than a direct link from smoking to cancer). The problem is resolved if we introduce a new variable "Tar deposit levels" such that Smoking and Cancer are conditionally independent given Tar. Assuming that there is a causal link between smoking and tar deposit levels, and not vice versa, the causal structure is unambiguously determined as Smoking -> Tar -> Cancer. We can now compute the causal effect of smoking on cancer :).

(alternative formulation postulating new variables y)

## Summary and further questions

1. How do you extend a d-separation-duplicitous structure to a uniquely identifiable structure? What's the theory of d-separation equivalent DAGs.
2. Efficiently finding conditional independencies, and computing d-separation equivalence classes. Complexity classes of these problems.
3. Minimality vs priors etc. 
4. What if you don't have the full joint distribuion? Sampling bias stuff.
5. What does Pearl cite as **good applications** of his framework? (maybe check the Book of Why)
6. Where does conditional independence come in as the sole arbiter of consistency?
7. How does time fit into this?
8. Continuous variables?
9. Good intuitions for the various conditions, criteria and theorems?
