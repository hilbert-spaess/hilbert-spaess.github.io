<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## What is a model?

A **model** is a structure with which we can interpret sentences in a formal language $L$. Loosely, by interpretation we mean assigning a truth value to the sentence according to whether it holds in the model. In the familiar first-order language of sets, an example of a **sentence** $\phi$ is $(\exists y)(\forall x)(x \not \in y)$. An example of a model of the language of sets might be $$M = \{ \{1\}, \{1,2\} \}$$, interpreting the formal $\in$ relation with standard set inclusion. By inspection, $\phi$ is true according to its obvious M-interpretation. 

If $\phi$ is true according to $M$, then we write $M \models \phi$, which is read as "$M$ models $\phi$". For every sentence $\phi$, either $M \models \phi$ or $M \models \lnot \phi$. Alternatively, we might write $$M(\phi) \in \{0,1\}$$. This map can be construed as a sort of **logical homomorphism** between the sentences of $L$ and the elements of $$\{0,1\}$$, which is a map that co-operates with logical operations $\land, \lor, \lnot$. For example, $M(\phi_1 \land \phi_2) = M(\phi_1) \land M(\phi_2)$.

This post concerns the possibility of logical homomorphisms to more complicated logical structures. To answer this question, we first need a precise definition of a logical structure.

## Boolean Algebras

A logical structure is a set equipped with constants 0 and 1, and operations $\land, \lor, \lnot$ satisfying the ordinary laws of logic. For example, the structure must satisfy the axiom for commutativity of $\land$: $x \land y = y \land x$, and the axiom of distributivity of $\lor$ over $\land$: $x \lor (y \land z) = (x \lor y) \land (x \lor z)$. There is no standard minimal set of axioms, so there is a choice of presentation.

The preferred presentation in model theory and algebra is as a particular sort of poset $(B, \leq)$, a **complemented distributive lattice**, usually referred to as a **Boolean algebra**. The relation $x \leq y$ is to be interpreted as $x \Rightarrow y = 1$. For example, the poset presentation of the trivial Boolean algebra $$\{0,1\}$$ is that $0 \leq 1$. Let's make this formal.

If $S \subset B$ is a subset of a poset $B$, then $u \in B$ is an **upper bound** for $S$ if for all $s \in S, s \leq u$. If $u \leq v$ for all other upper bounds $v$ of $S$, then $u$ is the **supremum** of $S$. We similarly define a **lower bound** and **infimum**. A **bounded lattice** is a poset for which every finite subset has a supremum and infimum. In this context we call the supremum a **join** and the infimum a **meet**. We write $\bigvee S$ for the meet of $S$ and $\bigwedge S$ for the join of $S$, and we write the join and meet of $$\{x,y\}$$ as $x \lor y$ and $x \land y$ respectively. We have $\bigwedge \emptyset = 1$ is a largest element, and $\bigvee \emptyset = 0$ is a smallest element. In a **distributive lattice**, we require that the meet and join operations satisfy the axioms of distributivity. Finally, in a **complemented distributive lattice**, for every $a \in B$ there is a complement $\lnot a \in B$ satisfying $a \lor \lnot a = 1$ and $a \land \lnot a = 0$. It can be shown that complements are unique. The succinct name for a complemented distributive lattice is a **Boolean algebra**. The powerset of a given set is a canonical example of a Boolean algebra, ordered under inclusion, with meet, join, and negation interpreted as intersection, union, and complement. Another example is the set of sentences in a first-order language, ordered under syntactic implication, with meet, join and negation interpreted as formal conjuction, disjunction and negation.

The emphasis on the partial order of implication is unintuitive if your primary experience of logical operations is with circuit gates and truth tables. But when making the leap to intermediary truth values, the partial order is actually a useful mental scaffold. If $a < b$, then $b$ is a more stringent notion of truth, so that $b \Rightarrow a = 0$. You can't derive a weak truth from a strong truth.

A final note: a Boolean algebra is **complete** if arbitrary sets (not just finite sets) have meets and joins. Complete Boolean algebras will be useful when thinking about universal quantification: interpreting $\forall$ will involve taking a join of a (maybe big) arbitrary set.  

## Boolean-valued models

Just as ordinary models are structures that entail a logical homomorphism between a language and $$\{0,1\}$$, Boolean-valued models (BVMs) are structures entailing logical homomorphisms between a first-order language and an arbitrary Boolean algebra. Let's make this precise.

Recall that a first-order language consists of a set of function symbols $\Omega$, a set of relation symbols $\Pi$, and the set of sentences $\mathcal{L}$. As set theory is our primary interest, for now we assume that $\Omega$ is empty. Indeed, in the language of set theory, $\Omega = \emptyset$, and $\Pi$ contains only the binary relation $\in$. Let $\mathbb{B}$ be a complete Boolean algebra. Our BVM will consist of a set $A$, with which we define a map $$\| . \| \to \mathbb{B}$$, sending each $\phi \in \mathcal{L}$ to a truth value $$\|\phi\| \in \mathbb{B}$$.

For all $x, y \in A$, we specify $$\| x = y \|$$, the truth value for the equality predicate. We also specify $$\| \pi(x_1, ...., x_n)\|$$ for all $\pi \in \Pi$. Having thus defined the logical homomorphism on atomic formulae, we extend it to all of $\mathcal{L}$ by induction on formula complexity. The completeness of $\mathbb{B}$ is necessary only when defining universal quantification. We define $$\|(\exists x)\phi(x)\| = \bigvee_{a \in A}\|\phi(a)\|$$, and $$\| (\forall x) \phi(x) \| = \bigwedge_{a \in A} \| \phi(a) \| $$.

With ordinary models $M$ we would write $M \models \phi$ if $M(\phi) = 1$. For a BVM $A$, we say that $\phi$ is **valid according to $A$** if $$\|\phi\| = 1$$. In order for this notion of validity to be an adequate generalisation of standard semantic entailment, we need it to co-operate with syntactic entailment. In particular, we want the axioms of first-order logic to be valid according to $A$, and the syntactic consequences of valid statements to also be valid. The axioms referring to quantification, implication and pure propositional logic are valid by virtue of the map being a logical homomorphism. The only axioms that are not necessarily satisfied are those referring to the equality predicate. We thus add the following constraints to the map as defined on atomic formulae. For all $x,y \in A$, we require:

$$(1)\,  \| x = x \| = 1 $$  
$$(2)\, \|(x = y) \Leftrightarrow (y = x)\| = 1$$, or $$ \| x = y \| = \| y = x \| $$  
$$(3)\,  \| (x = y) \land (y = z) \Rightarrow (x = z)\| = 1$$, or $$ \| x = y \| \land \| y = z \| \leq \|x = z \| $$

Note the useful rephrasing in terms of the partial order. These guarantee that equality behaves like an equivalence relation. Finally, we insist that equality co-operates with variable substitution. For all $x,y \in A$, and $\pi \in \Pi$, we require

$$(4)\, \| x_1 = y_1 \| \land \|\phi(x_1, ..., x_n)\| \leq \| \phi(y_1, ..., x_n) \| $$.

To recap, a BVM consists of a complete Boolean algebra $\mathbb{B}$, and a non-empty set $A$, with a logical homomorphism $$\| . \|$$ defined on the atomic formulae of $\mathcal{L}$, and satisfying $(1)-(4)$. If these are satified, it is an easy proof that the axioms of first-order logic are valid, and the rules of inference applied to valid sentences yield valid sentences. This means we have a form of soundness: provable sentences are valid in all BVMs. So if the axioms of a first-order theory are valid in a BVM, and a sentence $\phi$ has $$\| \phi \| \not \in \{0,1\}$$, then $\phi$ is independent of the axioms. This gives an inkling of the utility of BVMs for consistency proofs.

The set $A$ itself is an interesting beast. Distinct elements $x,y \in A$ can nevertheless satisfy $$\| x = y \| = 1$. As such, its elements are not referred to as objects, but as **names**. This is a nod to the fact that distinct names can refer to the same object.

## The standard Boolean-valued model of ZFC

Given a Boolean algebra $\mathbb{B}$, can we construct a BVM that models ZFC and takes values in $\mathbb{B}$? Of course, we presume access to the standard set-theoretic universe $V$. It turns out a fairly intuitive construction yields a proper class that is interpretable as a Boolean model. As such, not only is it fairly straightforward to find such a BVM, but the model is a class that is definable in the base model $V$. 

Our model $V^{\mathbb{B}}$ will consist of 'Boolean-valued sets'. A Boolean-valued set $x$ is a function from a domain of possible elements $\mathcal{D}(x)$ to $\mathbb{B}$, expressing the degree to which the elements of $\mathcal{D}(x)$ are members of $x$. Of course, $\mathcal{D}(x)$ a set in $V$ and the function $x$ is a function in $V$. Formally, by analogy with the construction of the Von Neumann hierarchy, we build the class $V^{\mathbb{B}}$ by transfinite recursion:

$$ V_0^{\mathbb{B}} = \emptyset $$  
$$ V_{\alpha^{+}}^{\mathbb{B}} = \{ f : \mathcal{D}(x) \to \mathbb{B} \, | \, \mathcal{D}(x) \subset V_{\alpha}^{\mathbb{B}} \} $$  
$$ V_{\lambda}^{\mathbb{B}} = \bigcup_{\gamma < \lambda} V_{\gamma}^{\mathbb{B}} $$

The class $V^{\mathbb{B}} = \bigcup_{\alpha} V_{\alpha}^{\mathbb{B}}$ is the candidate BVM. The definitions of $$\| x \in y \|, \| x = y \|$$ are now natural. For example, when checking membership $$\|x \in y \|$$, we have to consider both the degree to which $x$ is equal to an element of $y$, and the degree to which this element is indeed a member of $y$. As in the usual hierarchy $V$, we define the **rank** of $x \in V^{\mathbb{B}}$ inductively. The following definitions are by double recursion on the ranks of $x$ and $y$: 

$$ \| x \in y \| = \bigvee\limits_{z \in \mathcal{D}(y)} \| x = z \| . y(z) $$  
$$ \| x \subset y \| = \bigwedge\limits_{z \in \mathcal{D}(x)} \| z \in x \| \Rightarrow y(z) $$  
$$ \| x = y \| = \| x \subset y \| . \| y \subset x \| $$

To show that this is a full-blooded BVM, we need to verify $(1)-(4)$. Let's verify that $$\| x = x \| = 1$$. The remainder of the axioms have similar proofs. We prove by induction. $$ \| x \subset x \| = \bigvee\limits_{z \in \mathcal{D}(x)}x(z) \Rightarrow \|z \in x \|$$. But by induction for all $z \in \mathcal{D}(x)$, $x(z) = \| z = z\| \land x(z) \leq \|z \in x \|. \qed$$

## Quotienting out $V^B$

When studying the model theory of set theory, ordinary models are the primary objects of study. The goal of the technique of forcing is the construction of new legitimate models of ZFC with interesting properties. How can we use $V^B$ to build a new ordinary model of ZFC?

If we want to get **objects** from **names**, we might want to try quotienting $V^B$ according to the Boolean-valued equality and containment predicates. One idea is to define equivalence classes by:

$$ [x] (=) [y] \Leftrightarrow \| x = y \| = 1 $$  
$$ [x] (\in) [y] \Leftrightarrow \| x \in y \| = 1 $$

We define $$V^B/\{1\} = \{[x] : x \in V_B \}$$. It's easily checked that the containment predicate on equivalence classes co-operates with the equality predicate, so $$(V^B/\{1\}, (=), (\in) )$$ is a fully-fledged model of the language of set theory. It remains to check that this is not only a model of ZFC, but is in fact a new model of ZFC. 

## Quotienting by a general ultrafilter



## Building $V[G]$