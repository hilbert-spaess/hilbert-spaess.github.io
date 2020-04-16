<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

I've found a lot of good resources motivating MCMC methods, and describing the relevant algorithms, chiefly Gibbs sampling, Metropolis sampling, and Hybrid Monte-Carlo. When attempting to actually apply these tools, I've come across a few tricks and concepts that weren't clearly signposted in the literature. (The specific problems that required the use of MCMC were [survival curves](https://hilbert-spaess.github.io/STATS-survival-curves/) problems and full parameter inference of neural network models).

## Brief motivation and intuition

Assume we have a distribution $P(\theta)$ over a high-dimensional vector of parameters $\theta$. We want to get some decent independent samples of $\theta$. We often assume that $P$ is un-normalised, and we don't know the normalisation constant. Simple approaches like discretizing the parameter space scale badly with increasing dimension. In fact, if the distribution is a posterior distribution on a parameter we're interested in, we hope that the probability is concentrated in a small region of the space. This gives the problem an optimisational flavour- we're looking for the peaks of a complicated probability density function. If we were looking for the point of maximum density, an algorithm like gradient ascent might be useful.

Since we're looking for a sample, and not the maximum a posteriori estimate, we can follow an analagous tactic, by following an 'approximate gradient ascent' that is calibrated to result in a sample. Formally, we follow a Markov chain that tends to a sample from the target distribution. Without going into detail, we assume that this is achieved if the target distribution is invariant under the Markov chain.


----

**Idea:** Carry out a biased random walk around the parameter space. This will be useful for the same reason that gradient descent is useful. Formalised as a Markov chain under which the target distribution is invariant.

----

Again, without getting too fussy about details, there's a simple condition called **detailed balance** for deciding if the target distribution is indeed invariant under the proposed Markov chain. We say that the target distribution $P$ and transition function $Q(\theta_i \vert \theta_j)$ satisfy detailed balance if for all $\theta_i, \theta_j$, we have 

$$P(\theta_i) Q(\theta_j \vert \theta_i) = P(\theta_j) Q(\theta_i \vert \theta_j)$$.

The prototypical example of a transition function satisfying detailed balance is the Metropolis update rule. We start by choosing a **proposal function** $Q(\theta_i \vert \theta_j)$, a symmetric transition that admits straightforward sampling, such as a Gaussian centred at $\theta_i$. To sample from the Metropolis transition function, we first sample $\theta_j$ from this proposal function, and accept this proposal with probability $\min{\{\frac{P(\theta_j)}{P(\theta_i)}, 1\}}$. 

Taking a Gaussian proposal function, the choice of radius exhibits an important trade-off. A larger radius allows the chain to potentially traverse the parameter space much more quickly. But the larger the radius, the smaller the chance that the proposal will be accepted, as the chain attempts to lurch out to regions of substantially lower probability. 

---
**Idea:** Detailed balance is a useful condition to guarantee theoretical convergence. Most MCMC methods have transition functions that satisfy detailed balance. The speed at which these chains actually approach the target distribution is dependent on choices such as the proposal radius.---


## Chains-within-chains

## ARS

## Dimension-jumping

## Checking everything's working
