<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is the first post in a projected multi-post sequence on **forcing** and its use in independence proofs in set theory. I'm hoping to take the sequence in a philosophical direction, but this is an area of philosophy for which quite a lot of (thankfully attractive) maths is needed. The intended pre-requisites are an understanding of first-order logic up to the completeness theorem. [Written by a beginner etc].

## What is a model?

A model is a structure with which we can interpret sentences in a formal language. Loosely, by interpretation we mean assigning a truth value to the sentence according to whether it holds in the model. In the familiar first-order language of sets, an example of a **sentence** $\phi$ is $(\exists y)(\forall x)(x \not \in y)$. An example of a model of the language of sets might be $M$ = \{ \{1\}, \{1,2\} \}, interpreting the formal $\in$ relation as standard set inclusion. By inspection, $\phi$ is true according to its obvious M-interpretation. 

Let's recall the inductive definition of M-interpretation $\phi_M$ of a sentence $\phi$, for an arbitrary first-order language $L$, with function constants $\Omega$ and relation constants $\Pi$. Functions $f \in \Omega$ and relations $r \in \Pi$ have interpretations as function and relation $f_A$ and $r_A$ on $M$ as a set. [Define atomic formulae]. [Define truth values of full sentences by inspection on the model.]

[Assigning truth values to atomic formulae, then extrapolating].

[Soundness and completeness]

[Multi-valued notion of truth. Need corresponding and, or, and not. The correct structure here is a Boolean algebra.

## An application of BVMs to propositional logic

Let's show that Boolean-valued models can be used to solve an interesting problem in propositional logic.

We start with the simpler language of propositional logic. This consists of a family of **primitive propositions** $P$, represented by symbols like $p,q,r$, which are the atomic formulae. The Boolean algebra $S$ of sentences consists arbitrary combinations of atomic formulae assembled with the usual logical connectives of $\land, \lor, \lnot$, and $\Rightarrow$. For the sake of simplicity, we note that limiting our connectives to $\Rightarrow$ and a 'False' symbol $\bot$ will be just as expressive. A standard model (or **valuation**) of propositional logic is a homomorphism of Boolean algebras between $S$ and the binary truth Boolean algebra \{True, False\}. Put simply, it assigns binary truth values to sentences while respecting the basic logical operations. It is easy to show that a valuation is uniquely determined by the values it assigns to primitive propositions. For example, if $v$ is a valuation such that $v(p) = 1$, $v(q) = 0$, then $v(p \Rightarrow q) = 0$. A general Boolean-valued model is a straightforward extension: a homomorphism between $S$ and an arbitrary Boolean algebra $B$.

The usual axiomatisation of propositional logic consists of the following three axiom schema, formed by substituting $p,q,r$ in what follows with all possible combinations of elements of $S$:

$$p \Rightarrow (q \Rightarrow p)$$  
$$[ p \Rightarrow (q \Rightarrow r)] \Rightarrow [(p \Rightarrow q) \Rightarrow (p \Rightarrow r)]$$  
$$ p \Rightarrow (\lnot \lnot p)$$

We ask the following question: does there exist a theorem of propositional logic, consisting only of primitive propositions and the connective $\Rightarrow$, such that it cannot be proved using only the first two axiom schema?

If there does exist such a sentence $\phi$, we are being asked to prove an *independence statement*: we are being asked to show that $\phi$ is independent of the first two axiom schema. The usual model-based approach to proving independence is to use the soundness theorem. For any (standard) valuation of propositional logic, if the valuation assigns truth value 1 to a set of axioms, it assigns 1 to all provable consequences. Thus, if we can find a valuation in which all axioms of the first two schema take value 1, but $\phi$ takes value 0, we have shown that $\phi$ cannot be deduced from these axioms alone. The problem is that if $\phi$ is a theorem of propositional logic, it will take value 1 in *any* valuation, so this argument is doomed to fail.


## The standard Boolean-valued model of set theory

## Quotienting by a filter

## Building V[G]