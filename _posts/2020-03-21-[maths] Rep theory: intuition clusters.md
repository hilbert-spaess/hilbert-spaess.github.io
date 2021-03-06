---
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

As outlined here, I'm trying to develop understanding by doing spaced repetition learning on 'intuition clusters'. There's an accompanying Anki deck for this summary.

## Basic rep theory

#### Reps of a finite group over a complex vector space.

* **Def:** group hom $\rho : G \to GL(V)$. The **degree** is $\dim{V}$.
* A collection of linear maps on a f.d. complex vector space with a group structure.
    * Requires intuition for linear maps on f.d. vector space; finite groups.
* A functor from $G$ considered as a category (with a single object) to the category **Vect** of complex vector spaces.
* **Examples**
    * A rep of $C_n$: a matrix of order $n$, and its powers.
    * $D_6$: matrices corresponding to rotations and reflections in $\mathbb{R}^2$.
    * $\mathbb{C}X$: permutation matrices corresponding to a G-action on $X$, for any group $G$.
 * <font color = 'red'> Reps are basically finite matrix groups; functor from G to Vect </font>
   
#### Subreps, irreducibility, direct sum

Subrep

* **Def:** a subrepresentation is a G-invariant subspace $$W$$ of $$V$$.
* The linear maps restricted to this subspace also form a rep of $$G$$.
* **Def:** a representation with no proper subreps is an irreducible rep.
* Irreducible rep examples
    * Any one-dimensional rep is irreducible.
    * Only irreps of $$C_n$$ are one-dimensional. Pick an eigenvector $$v$$ of $$\rho(1)$$. Then $$\langle v \rangle$$ is a G-invariant subspace.
* **Def:** $$V$$ is a **direct sum** of subreps $$U$$ and $$W$$ if $$V = U \oplus W$$.
* If $$V$$ is a direct sum, there is a basis of $$W$$ and a basis of $$U$$ such that with respect to the union of these bases, $$\rho(g)$$ is always block diagonal.
* **Theorem**: if $$W$$ is a subrep, there is a complementary subrep $$U$$ such that $$V = U \oplus W$$.
    * This will follow from existence of G-invariant inner product (see below).
* So Maschke means that we have complete reducibility: we can always decompose a representation as a direct sum of irreducible reps.
* <font color = 'red'> Subrep is subspace that's also rep; irreps are primitive, indivisible; every subrep part of a direct sum decomposition into irreps
   
#### G-linear maps

* **Def**: given $$(\rho, V), (\rho', W)$$ are reps of $$G$$, a G-linear map is a linear map $$\phi : V \to W$$ such that $$\phi \circ \rho(g) = \rho'(g) \circ \phi$$ for all $$g \in G$$.
* A linear map between representations that co-operates with the group structure.
* A natural transformation between the representations considered as functors.
* **Def:** If there is a G-linear isomorphism between $$V$$ and $$W$$, we say that they are isomorphic as representations.
* Isomorphic representations are representations of $$G$$ that are related by a change of basis.
* **Theorem:** Suppose $\phi$ is a G-linear map $V \to W$. Then $G/\ker{\phi}$ and $\im{\phi}$ are iso as reps. (First isomorphism theorem for reps).
* Same intuition as other first isomorphism theorems. 
* **Def:** let $G(V,W)$ denote the vector space of G-linear maps $V \to W$. Then we can turn it into a rep of $G$ via $(g. \phi)(v) = \phi(g^{-1}.v)$, for all $\phi \in G(V,W)$.
* Just like translating a function $\mathbb{R} \to \mathbb{R}$ by 1: $(+1)(f)(x) f(x-1)$. We can act on G-linear maps by $G$ by 'transforming' $V$ according to $g$.
* **Examples**
* <font color = 'red'> Natural transormations of reps as functors; clear choice of arrow in the category of reps; linear maps that co-operate with g-structure. </font>

#### G-invariant inner products, Weyl's trick

* **Def:** a G-invariant inner product is a Hermitian inner product $$\langle -,- \rangle$$ on $V$ such that $\langle x, y \rangle = \langle gx, gy \rangle$, $\forall g \in G$. 
* With respect to an orthonormal basis for this inner product, $\rho(g)$ is always in $U(n)$. 
* **Theorem:** you can always find a G-invariant inner product. So you can always pick a basis w.r.t. which $\rho(g)$ is unitary.
* There's always a way of looking at our space so that the group under consideration acts in a distance-preserving manner.
* We find the G-invariant inner product by 'g-averaging' w.r.t. a different inner product. Precisely, if $(x,y)$ is the standard inner product, we define $\langle x, y \rangle = \frac{1}{\vert G \vert}\sum_{g \in G}\(gx, gy)$. 
* The existence of the G-invariant inner product easily implies Maschke and complete reducibility: for a subrep, its orthogonal complement is also a subrep.

#### Schur's lemma; counting irreducible components

* **Theorem:** If $V$ and $W$ are irreps, then any G-linear map between $V$ and $W$ is the zero map or an isomorphism.
* Irreps are 'rigid' - there are no non-trivial G-linear maps between irreps.
* **Theorem:** Any two isomorphisms between irreps are scalar multiples of one another. 
* Isomorphic irreps are uniquely/canonically isomorphic.
* Any isomorphism $V \to V$ is a scalar multiple of the identity.
* **Theorem:** Suppose we decompose $V$ as $\oplus{i=1}^r V_i$. Then for each irrep $W$, $\vert \{i : V_i \cong W\} \vert = \dim{G(V,W)}$. 
* This is a generalisation of Schur's lemma. If $\phi$ is G-linear $V \to W$, then every irreducible component of $V$ that isn't isomorphic to $W$ gets sent to zero, and those that are isomorphic have a canonical iso. So $\phi$ is a linear combination of these canonical isos.
* We can write $V \cong \oplus n_i V_i$, where the $n_i$ are determined above.
* Irreducible decomposition satisfies uniqueness of isotypical decomposition.

## Character Theory

#### Characters

* **Def:** The character $\chi$ of $\rho$ is the trace of $\rho$. 
* Single one-dimensional property of a representation that will in fact be enough to determine a rep up to isomorphism. Want it to be an invariant of equivalent representations, which the trace clearly is. Trace behaves nicely with respect to addition and tensor product.
* $\chi$ is constant on conjugacy classes of $G$ (follows from trace being an invariant of equivalent reps, which we wanted above). 
* $\chi$ can be found as the sum of the eigenvalues. All eigenvalues are roots of unity, so $\chi$ is sum of roots of unity (hence algebraic integer etc). This formula gets us character of inverses: $\chi(g^{-1}) = \bar{\chi(g)}$. Character of identity: $\chi(e) = \dim{V}$.
* **Examples**

#### Space of class functions

* **Def:** The vector space $C(G)$ of **class functions** is the space of functions $G \to \mathbb{C}$ that are constant on conjugacy classes of $G$.
* Characters are class functions. We care about the space of class functions because we see that characters of irreps form a basis for the space.
* There is a natural inner product on $C(G)$, namely $\langle f, f' \rangle = \frac{1}{\vert G \vert}\sum_{g \in G}f(g) \bar{f'(g)}$.
* The **class delta functions** are $\delta_{O_i} \in C(G)$ for conjugacy classes $O_i$. They are 1 on $O_i$ and zero on all other conjugacy classes. They form a basis for $C(G)$, but not an orthonormal basis. Weighting by the size 

#### Character orthogonality + character tables

* **Theorem:** If $V, W$ are irreps of $G$, then $\dim{G(V,W)} = \langle \chi_V, \chi_W \rangle$. So by Schur, irreps are orthonormal class functions.
* The orthonormality of irreducible representations is captured by the orthonormality of characters.
* In fact, if $V = \oplus_{i=1}^r n_iV_i$, then $n_i = \langle \chi_V, \chi_{V_i}$. So $\chi_V$ determines the irreducible decomposition of $V$, and we have that the character of a rep determines the rep up to equivalence.
* $\langle \chi_V, \chi_V \rangle = 1$ iff V is irreducible.
* **Theorem:** The irreducible characters span $C(G)$, so they form a basis for $C(G)$. Therefore the number of irreps is the number of conjugacy classes of $G$.
* The **character table** is a matrix with rows the irreducible characters of $G$, and columns the conjugacy classes of $G$. The character table is a square. By orthogonality of irreducible characters, the rows are orthonormal.
* A column is real iff the conjugacy class is self-inverse.
* **Theorem:** Column orthogonality: the (standard) inner product of different columns is 0 if the columns are distinct, and $\vert C_G(g) \vert$ otherwise. In particular, $\sum_{i=1}^r\dim{V_i}^2 = \vert G \vert$.

#### Character table computations

* **Theorem:** Suppose $\chi$ is the character of $\mathbb{C}X$. Then $\chi(g)$ is the number of fixed points of the G-action on X. This is clear by summing the 1s on the main diagonal of g.
* Consider the regular representation $\mathbb{C}G$. The character is 0 for all $g \neq e$, because the action of $G$ on itself is faithful. Then $n_i = \langle \chi_{\mathbb{C}G}, \chi_i \rangle = \chi_i(e) = \dim{V_i}$. 
* For permutation reps, the data "# of fixed points" determines the rep up to isomorphism.

## Building new representations

#### Duality

#### Tensor products

####

