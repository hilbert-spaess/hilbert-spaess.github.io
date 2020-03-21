---
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

As outlined here, I'm trying to develop understanding by doing spaced repetition learning on 'intuition clusters'. There's an accompanying Anki deck for this summary.

## Basic rep theory

#### Reps of a finite group over a complex vector space.

* **Def:** group hom $\rho : G \to GL(V)$. The **degree** is $\dim{V}$.
* **Intuition:** a collection of linear maps on a f.d. complex vector space with a group structure.
    * Requires intuition for linear maps on f.d. vector space; finite groups.
* **Intuition**: a functor from $G$ considered as a category (with a single object) to the category **Vect** of complex vector spaces.
* **Examples**
    * A rep of $C_n$: a matrix of order $n$, and its powers.
    * $D_6$: matrices corresponding to rotations and reflections in $\mathbb{R}^2$.
    * $\mathbb{C}X$: permutation matrices corresponding to a G-action on $X$, for any group $G$.
 * **Fuzzy**
   
#### Subreps, irreducibility, direct sum

* Def: a subrepresentation is a G-invariant subspace $$W$$ of $$V$$.
* The linear maps restricted to this subspace also form a rep of $$G$$.
* Def: a representation with no proper subreps is an irreducible rep.
* Irreducible rep examples
    * Any one-dimensional rep is irreducible.
    * Only irreps of $$C_n$$ are one-dimensional. Pick an eigenvector $$v$$ of $$\rho(1)$$. Then $$\langle v \rangle$$ is a G-invariant subspace.
* Def: $$V$$ is a **direct sum** of subreps $$U$$ and $$W$$ if $$V = U \oplus W$$.
* If $$V$$ is a direct sum, there is a basis of $$W$$ and a basis of $$U$$ such that with respect to the union of these bases, $$\rho(g)$$ is always block diagonal.
* **Theorem**: if $$W$$ is a subrep, there is a complementary subrep $$U$$ such that $$V = U \oplus W$$.
    * This will follow from existence of G-invariant inner product (see below).
* So Maschke means that we have complete reducibility: we can always decompose a representation as a direct sum of irreducible reps.

#### G-linear maps

* **Def**: given $$(\rho, V), (\rho', W)$$ are reps of $$G$$, a G-linear map is a linear map $$\phi : V \to W$$ such that $$\phi \circ \rho(g) = \rho'(g) \circ \phi$$ for all $$g \in G$$.
* **Intuition:** A linear map between representations that co-operates with the group structure.
* **Intuition:** A natural transformation between the representations considered as functors.
* **Def:** If there is a G-linear isomorphism between $$V$$ and $$W$$, we say that they are isomorphic as representations.
* **Intuition:** Isomorphic representations are representations of $$G$$ that are related by a change of basis.
* **Theorem:** Suppose $\phi$ is a G-linear map $V \to W$. Then $G/\ker{\phi}$ and $\im{\phi}$ are iso as reps. (First isomorphism theorem for reps).
* **Intuition:** Same intuition as other first isomorphism theorems. 
* **Def:** let $G(V,W)$ denote the vector space of G-linear maps $V \to W$. Then we can turn it into a rep of $G$ via $(g. \phi)(v) = \phi(g^{-1}.v)$, for all $\phi \in G(V,W)$.
* **Inutuition:** Just like translating a function $\mathbb{R} \to \mathbb{R}$ by 1: $(+1)(f)(x) f(x-1)$. We can act on G-linear maps by $G$ by 'transforming' $V$ according to $g$.
* **Examples**

#### G-invariant inner products, Weyl's trick

* **Def:** a G-invariant inner product is a Hermitian inner product $$\langle -,- \rangle$$ on $V$ such that $\langle x, y \rangle = \langle gx, gy \rangle$, $\forall g \in G$. 
* **Intuition**: with respect to an orthonormal basis for this inner product, $\rho(g)$ is always in $U(n)$. 
* **Theorem:** you can always find a G-invariant inner product. So you can always pick a basis w.r.t. which $\rho(g)$ is unitary.
* **Intuition**: there's always a way of looking at our space so that the group under consideration acts in a distance-preserving manner.
* **Intuition**: we find the G-invariant inner product by 'g-averaging' w.r.t. a different inner product. Precisely, if $(x,y)$ is the standard inner product, we define $\langle x, y \rangle = \frac{1}{\vert G \vert}\sum_{g \in G}\(gx, gy)$. 
* **Intuition**: the existence of the G-invariant inner product easily implies Maschke and complete reducibility: for a subrep, its orthogonal complement is also a subrep.

#### Schur's lemma; counting irreducible components

* **Theorem:** If $V$ and $W$ are irreps, then any G-linear map between $V$ and $W$ is the zero map or an isomorphism.
* **Intuition:** Irreps are 'rigid' - there are no non-trivial G-linear maps between irreps.
* **Theorem:** Any two isomorphisms between irreps are scalar multiples of one another. 
* **Intutition:** Isomorphic irreps are uniquely/canonically isomorphic.
* **Intuition:** Any isomorphism $V \to V$ is a scalar multiple of the identity.
* **Theorem:** Suppose we decompose $V$ as $\oplus{i=1}^r V_i$. Then for each irrep $W$, $\vert \{i : V_i \cong W\}\vert = \dim{G(V,W)}$. 
* **Intuition:** This is a generalisation of Schur's lemma. If $\phi$ is G-linear $V \to W$, then every irreducible component of $V$ that isn't isomorphic to $W$ gets sent to zero, and those that are isomorphic have a canonical iso. So $\phi$ is a linear combination of these canonical isos.
* **Intuition:** We can write $V \cong \oplus n_i V_i$, where the $n_i$ are determined above.
* **Intution:** Irreducible decomposition satisfies uniqueness of isotypical decomposition.

## Character Theory

