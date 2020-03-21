---
layout: post
---

<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

### Basic rep theory

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

#### G-invariant inner products, Weyl's trick

* **Def:** a G-invariant inner product is a Hermitian inner product $$\langle -,- \rangle$$ on $V$ such that $\langle x, y \rangle = \langle gx, gy \rangle$, $\forall g \in G$. 
* **Intuition**: with respect to an orthonormal basis for this inner product, $\rho(g)$ is always in $U(n)$. 
* **Theorem:** you can always find a G-invariant inner product. So you can always pick a basis w.r.t. which $\rho(g)$ is unitary.
* **Intuition**: there's always a way of looking at our space so that the group under consideration acts in a distance-preserving manner.
* **Intuition**: we find the G-invariant inner product by 'g-averaging' w.r.t. a different inner product. Precisely, if $(x,y)$ is the standard inner product, we define $\langle x, y \rangle = \frac{1}{\vert G \vert}\sum_{g \in G}\langle gx, gy \rangle$. 

### Character Theory

