<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## What is a model?

A **model** is a structure with which we can interpret sentences in a formal language $L$. Loosely, by interpretation we mean assigning a truth value to the sentence according to whether it holds in the model. In the familiar first-order language of sets, an example of a **sentence** $\phi$ is $(\exists y)(\forall x)(x \not \in y)$. An example of a model of the language of sets might be $$M = \{ \{1\}, \{1,2\} \}$$, interpreting the formal $\in$ relation as standard set inclusion. By inspection, $\phi$ is true according to its obvious M-interpretation. 

If $\phi$ is true according to $M$, then we write $M \models \phi$, which is read as "$M$ models $\phi$". For every sentence $\phi$, either $M \models \phi$ or $M \models \lnot \phi$. Alternatively, we might write $$M(\phi) \in \{0,1\}$$. This map can be construed as a sort of **logical homomorphism** between the sentences of $L$ and the elements of $$\{0,1\}$$, which is a map that preserves logical operations $\land, \lor, \lnot$. For example, $M(\phi_1 \land \phi_2) = M(\phi_1) \land M(\phi_2)$.

The question arises as to whether we can define logical homomorphisms to more complicated logical structures. To answer, this question, we first need to 

## An application of BVMs to propositional logic

Let's show that Boolean-valued models can be used to solve an interesting problem in propositional logic.

We start with the simpler language of propositional logic. This consists of a family of **primitive propositions** $P$, represented by symbols like $p,q,r$, which are the atomic formulae. The Boolean algebra $S$ of sentences consists arbitrary combinations of atomic formulae assembled with the usual logical connectives of $\land, \lor, \lnot$, and $\Rightarrow$. For the sake of simplicity, we note that limiting our connectives to $\Rightarrow$ and a 'False' symbol $\bot$ will be just as expressive. A standard model (or **valuation**) of propositional logic is a homomorphism of Boolean algebras between $S$ and the binary truth Boolean algebra \{True, False\}. Put simply, it assigns binary truth values to sentences while respecting the basic logical operations. It is easy to show that a valuation is uniquely determined by the values it assigns to primitive propositions. For example, if $v$ is a valuation such that $v(p) = 1$, $v(q) = 0$, then $v(p \Rightarrow q) = 0$. A general Boolean-valued model is a straightforward extension: a homomorphism between $S$ and an arbitrary Boolean algebra $B$.

The usual axiomatisation of propositional logic consists of the following three axiom schema, formed by substituting $p,q,r$ in what follows with all possible combinations of elements of $S$. (These axiom schema suffice for completeness of propositional logic).

$$ p \Rightarrow (q \Rightarrow p) $$  
$$ [ p \Rightarrow (q \Rightarrow r)] \Rightarrow [(p \Rightarrow q) \Rightarrow (p \Rightarrow r)] $$  
$$ (\lnot \lnot p) \Rightarrow p $$

We ask the following question: does there exist a theorem of propositional logic, consisting only of primitive propositions and the connective $\Rightarrow$, such that it cannot be proved using only the first two axiom schema?

If there does exist such a sentence $\phi$, we are being asked to prove an *independence statement*: we are being asked to show that $\phi$ is independent of the first two axiom schema. The usual model-based approach to proving independence is to use the soundness theorem. For any (standard) valuation of propositional logic, if the valuation assigns truth value 1 to a set of axioms, it assigns 1 to all provable consequences. Thus, if we can find a valuation in which all axioms of the first two schema take value 1, but $\phi$ takes value 0, we have shown that $\phi$ cannot be deduced from these axioms alone. The problem is that if $\phi$ is a theorem of propositional logic, it will take value 1 in *any* valuation, so this argument is doomed to fail.

However, general BVMs will come to our rescue. A version of soundness also holds for valuations taking values in an arbitrary Boolean algebra. If a sentence is a logical consequence of a set of axioms assigned truth value 1, then the sentence will be assigned truth value 1. So if we can exhibit a Boolean-valued model of the first two axiom schema, for which the value assigned to $\phi$ is not 1, we will have shown the desired independence. Let's consider the next simplest Boolean algebra after binary truth. This has four elements, with two new 'midway' truth values $a$ and $b$ satisfying $a = \lnot b$ (this Boolean algebra has the structure of the powerset of a two-element set). We will call a valuation taking values in this structure a 4-valuation. Note first that any 4-valuation models the first two axiom schema.

Let's now guess a theorem of propositional logic that might require the third axiom for a proof. We expect such a sentence to indirectly appeal to the law of the excluded middle- an informal proof will split into cases according to whether a given proposition is true or false. A candidate is:  

$$ p \Rightarrow ((p \Rightarrow p) \Rightarrow p)$$

Indeed, this holds for 'different reasons' for different (standard) valuations of $p$. It is thus a theorem of propositional logic, and by completeness is provable with the first three axiom schema. 

## BVMs in first-order logic

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