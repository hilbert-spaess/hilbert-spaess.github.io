<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is the first post in a projected multi-post sequence on **forcing** and its use in independence proofs in set theory. I'm hoping to take the sequence in a philosophical direction, but this is an area of philosophy for which quite a lot of (thankfully attractive) maths is needed. The intended pre-requisites are an understanding of first-order logic up to the completeness theorem, an understanding of the axioms of ZFC, and understanding of the basic model theory of ZFC (the Von Neumann hierarchy and Mostowski collapse). [Written by a beginner etc].

## What is a model?

A model is a structure with which we can interpret sentences in a formal language. Loosely, by interpretation we mean assigning a truth value to the sentence according to whether it holds in the model. In the familiar first-order language of sets, an example of a **sentence** $\phi$ is $(\exists y)(\forall x)(x \not \in y)$. An example of a model of the language of sets might be $M$ = \{ \{1\}, \{1,2\} \}, interpreting the formal $\in$ relation as standard set inclusion. By inspection, $\phi$ is true according to its obvious M-interpretation. 

Let's recall the inductive definition of M-interpretation $\phi_M$ of a sentence $\phi$, for an arbitrary first-order language $L$, with function constants $\Omega$ and relation constants $\Pi$. Functions $f \in \Omega$ and relations $r \in \Pi$ have interpretations as function and relation $f_A$ and $r_A$ on $M$ as a set. [Define atomic formulae]. [Define truth values of full sentences by inspection on the model.]

[Assigning truth values to atomic formulae, then extrapolating].

[Soundness and completeness]

[Multi-valued notion of truth. Need corresponding and, or, and not. The correct structure here is a Boolean algebra.

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

When defining $\|\|phi\|\|$ inductively, instances of conjuction, negation and so on are straightforwardly specified by ensuring that $\|\|.\|\|$ is a homomorphism of Boolean algebras. For example, $\|\|phi_1 \lor \phi_2\|\| = \|\|phi_1\|\| \lor \|\|phi_2\|\|$. Instances of quantification are more interesting. We define $\|\|(\exists x) \phi(x)\|\| = \lor_{a \in A}\|\|\phi(a)\|\|$, and (for all equivalent). For the right-hand sides to be well-defined, we require the condition that $B$ is complete. 

We say that a sentence $\phi$ is valid


## The standard Boolean-valued model of set theory

To constructConsider the universe of sets $V$. 

## Quotienting by a filter

## Building V[G]