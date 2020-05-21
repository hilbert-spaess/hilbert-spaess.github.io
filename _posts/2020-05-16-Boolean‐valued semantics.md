<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## What is a model?

A **model** is a structure with which we can interpret sentences in a formal language $L$. Loosely, by interpretation we mean assigning a truth value to the sentence according to whether it holds in the model. In the familiar first-order language of sets, an example of a **sentence** $\phi$ is $(\exists y)(\forall x)(x \not \in y)$. An example of a model of the language of sets might be $$M = \{ \{1\}, \{1,2\} \}$$, interpreting the formal $\in$ relation with standard set inclusion. By inspection, $\phi$ is true according to its obvious M-interpretation. 

If $\phi$ is true according to $M$, then we write $M \models \phi$, which is read as "$M$ models $\phi$". For every sentence $\phi$, either $M \models \phi$ or $M \models \lnot \phi$. Alternatively, we might write $$M(\phi) \in \{0,1\}$$. This map can be construed as a sort of **logical homomorphism** between the sentences of $L$ and the elements of $$\{0,1\}$$, which is a map that co-operates with logical operations $\land, \lor, \lnot$. For example, $M(\phi_1 \land \phi_2) = M(\phi_1) \land M(\phi_2)$.

The question arises as to whether we can define logical homomorphisms to more complicated logical structures. To answer this question, we first need a precise definition of a logical structure.

## Boolean Algebras

A logical structure is a set equipped with constants 0 and 1, and operations $\land, \lor, \lnot$ satisfying the ordinary laws of logic. For example, the structure must satisfy the axiom for commutativity of $\land$: $x \land y = y \land x$, and the axiom of distributivity of $\lor$ over $\land$: $x \lor (y \land z) = (x \lor y) \land (x \lor z)$. There is no standard minimal set of axioms, so there is a choice of presentation.

The preferred presentation in model theory and algebra is as a particular sort of poset $(B, \leq)$, a **complemented distributive lattice**, usually referred to as a **Boolean algebra**. The relation $x \leq y$ is to be interpreted as $x \Rightarrow y = 1$. For example, the poset presentation of the trivial Boolean algebra $$\{0,1\}$$ is that $0 \leq 1$. Let's make this formal.

If $S \subset B$ is a subset of a poset $B$, then $u \in B$ is an **upper bound** for $S$ if for all $s \in S, s \leq u$. If $u \leq v$ for all other upper bounds $v$ of $S$, then $u$ is the **supremum** of $S$. We similarly define a **lower bound** and **infimum**. A **bounded lattice** is a poset for which every finite subset has a supremum and infimum. In this context we call the supremum a **join** and the infimum a **meet**. We write $\bigvee S$ for the meet of $S$ and $\bigwedge S$ for the join of $S$, and we write the join and meet of $$\{x,y\}$$ as $x \lor y$ and $x \land y$ respectively. We have $\bigwedge \emptyset = 1$ is a largest element, and $\bigvee \emptyset = 0$ is a smallest element. In a **distributive lattice**, we require that the meet and join operations satisfy the axioms of distributivity. Finally, in a **complemented distributive lattice**, for every $a \in B$ there is a complement $\lnot a \in B$ satisfying $a \lor \lnot a = 1$ and $a \land \lnot a = 0$. It can be shown that complements are unique. The succinct name for a complemented distributive lattice is a **Boolean algebra**. The powerset of a given set is a canonical example of a Boolean algebra, ordered under inclusion, with meet, join, and negation interpreted as intersection, union, and complement. Another example is the set of sentences in a first-order language, ordered under syntactic implication, with meet, join and negation interpreted as formal conjuction, disjunction and negation.

The emphasis on the partial order of implication is unintuitive if your primary experience of logical operations is with circuit gates and truth tables. But when making the leap to intermediary truth values, the partial order is actually a useful mental scaffold. If $a < b$, then $b$ is a more stringent notion of truth, so that $b \Rightarrow a = 0$. You can't derive a weak truth from a strong truth.

A final note: a Boolean algebra is **complete** if arbitrary sets (not just finite sets) have meets and joins. Complete Boolean algebras will be useful when thinking about universal quantification: interpreting $\forall$ will involve taking a join of a (maybe big) arbitrary set.  

## Boolean-valued models

Boolean-valued models (BVMs) are logical homomorphisms between a first-order language and an arbitrary Boolean algebra. Let's make this precise.

We will now formally define a Boolean-valued model of a first-order language $L$. Recall that a first-order language consists of a set of function symbols $\Omega$, a set of relation symbols $\Pi$, and the 'arity' function $\alpha: \Omega \cup \Pi \to \mathbb{N}$. If $L$ is the language of set theory, then $\Omega = \emptyset$, and $\Pi$ contains only the binary relation $\in$. Let $B$ be a complete Boolean algebra. We want to define a model of $L$ so that sentences can be interpreted as taking truth values in $B$.

Let $B$ be a complete Boolean algebra. A Boolean-valued model of $L$ is a non-empty set $A$ with a function $f_A : A^n \to A$ for each $f \in \Omega, \alpha(f) = n$. So far, this is the same as the vanilla definition of a model. However, for a relation $\phi \in \Pi, \alpha(\phi) = n$, the claim $\phi(a_1, ..., a_n)$ is no longer either true or false. Instead, we write $\|\|\phi(a_1, ..., a_n)\|\|in B$ as the truth value of the relation. Here, for convenience, where interpretation takes values in $B$, we replace the subscript notation with 'norm' notation. So the interpretation of $\phi$ is $\|\| \circ \phi : A^n \to B$. In addition to interpretations for each relation in $\Pi$, the 2-ary relation = also requires an interpretation. For each $a_1, a_2 \in A$, regardless of whether $a_1, a_2$ are distinct elements, there will be a truth value to the claim $a_1 = a_2$, denoted by $\|\|a_1 = a_2\|\| \in B$. With the relation and function constants thus defined, we will build up the interpretation $\|\|\phi\|\|$ of an arbitrary sentence $\phi$ inductively. For example, if $L$ is the language of set theory, to specify a Boolean-valued model it suffices to specify, for each pair $a_1, a_2 \in A$, truth values $\|\|a_1 \in a_2\|\|$ and $\|\|a_1 = a_2\|\| \in B$.

When defining $\|\|\phi\|\|$ inductively, instances of conjuction, negation and so on are straightforwardly specified by ensuring that $\|\|.\|\|$ is a homomorphism of Boolean algebras. For example, $\|\|\phi_1 \lor \phi_2\|\| = \|\|\phi_1\|\| \lor \|\|\phi_2\|\|$. Instances of quantification are more interesting. We define $\|\|(\exists x) \phi(x)\|\| = \lor_{a \in A}\|\|\phi(a)\|\|$, and (for all equivalent). For the right-hand sides to be well-defined, we require the condition that $B$ is complete. 

We say that a sentence $\phi$ is *valid* if $\|\|\phi\|\| = 1$. We'd like the axioms of first-order logic to be valid for our model. Note that $\|\|\phi \Rightarrow \psi\|\| = 1 \Leftrightarrow \|\|\phi\|\| \leq \|\|\psi\|\|$. As with pure propositional logic, the propositional axioms are satisfied by virtue of the Boolean algebra homomorphism. The axioms referring to quantification and implication are also satisfied. The only axioms that aren't immediately satisfied are those referring to the equality predicate. To ensure that these are satisfied, we require that for all $x, y \in A$, and formulae $p$ with $y$ not occurring in $p$:

$$ \| x = x \| = 1 $$  
$$ \| x = y \| = \| y = x \| $$  
$$ \| x = y \| \land \| y = z \| \leq \|x = z \| $$  
$$ \| x = y \| \leq \| p \Rightarrow p[y/x] \| $$

These guarantee that the axioms concerning the equality relation are valid. In the case that $L$ is the language of set theory, the final axiom can be replaced with the more specific

$$\| x = v \| \land \|y = z\| \land \|x \in y \| \leq \|v \in z \|$$

So all axioms of first-order logic are valid in a Boolean-valued model. It is now easily verified that the rules of inference (generalisation and modus ponens) applied to valid sentences yield valid sentences. We thus have a form of soundness: provable sentences are valid in a Boolean-valued model. This means we can use Boolean-valued models for consistency proofs: if the axioms of a first-order theory are valid in a Boolean-valued model, and a sentence $\phi$ has $\|\| \phi \|\| \neq 0, 1$, then $\phi$ is independent of the axioms.

## The standard Boolean-valued model of ZFC

We've now seen the full definition of a Boolean-valued model of the first-order language of set theory. The question we now turn to is: given a Boolean algebra $B$, can we construct a Boolean-valued model of ZFC taking values in $B$? Of course, we need to assume access to a transitive model $V$ of ZFC. It turns out a fairly intuitive construction yields a proper class that is interpretable as a Boolean model.

Our model $V^B$ will consist of 'Boolean-valued sets'. A Boolean-valued set $x$ is a function from a domain of possible elements $\mathcal{D}(x)$ to $B$, expressing the 'degree of membership'. Of course, the domain is a set in $V$ and the function is a function in $V$. Formally, by analogy with the construction of the Von Neumann hierarchy, we build up $V^B$ by transfinite recursion:

$$ V_0^B = \emptyset $$

$$ V_{\alpha^{+}}^B = \{ f : x \to B | x \subset V_{\alpha} \} $$

$$ V_{\lambda}^B = \bigcup_{\gamma < \lambda} V_{\gamma}^B $$

The class $V^B = \cup_{\alpha} V_{\alpha}$ is our candidate Boolean-valued model. The definitions of $$\| x \in y \|, \| x = y \|$$ are now natural. For example, when checking membership $$\|x \in y \|$$, we have to consider both the degree to which $x$ is equal to an element of $y$, and the degree to which this element is indeed a member of $y$. The **rank** of $x \in V^B$ is defined by induction. The following definitions are by double recursion on the ranks of $x$ and $y$: 

$$ \| x \in y \| = \bigvee\limits_{z \in \mathcal{D}(y)} \| x = z \| . y(z) $$  
$$ \| x \subset y \| = \bigwedge\limits_{z \in \mathcal{D}(x)} \| z \in x \| \Rightarrow y(z) $$  
$$ \| x = y \| = \| x \subset y \| . \| y \subset x \| $$

It is easily checked that $V^B$ satisfies the axioms of a Boolean-valued model of set theory. There exist distinct elements $x,y$ of $V^B$ that nevertheless satisfy $$\| x = y \| = 1$$. For example, we could construct $y$ by adding a new element $z$ to the domain of $x$, such that $y(z) = 0$. For this reason, we refer to the elements of $V^B$ as **names**. Showing that the axioms of ZFC are valid for $V^B$ is not too challenging.

## Quotienting out $V^B$

When studying the model theory of set theory, ordinary models are the primary objects of study. The goal of the technique of forcing is the construction of new legitimate models of ZFC with interesting properties. How can we use $V^B$ to build a new ordinary model of ZFC?

If we want to get **objects** from **names**, we might want to try quotienting $V^B$ according to the Boolean-valued equality and containment predicates. One idea is to define equivalence classes by:

$$ [x] (=) [y] \Leftrightarrow \| x = y \| = 1 $$  
$$ [x] (\in) [y] \Leftrightarrow \| x \in y \| = 1 $$

We define $$V^B/\{1\} = \{[x] : x \in V_B \}$$. It's easily checked that the containment predicate on equivalence classes co-operates with the equality predicate, so $$(V^B/\{1\}, (=), (\in) )$$ is a fully-fledged model of the language of set theory. It remains to check that this is not only a model of ZFC, but is in fact a new model of ZFC. 

## Quotienting by a general ultrafilter



## Building $V[G]$