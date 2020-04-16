I've found a lot of good resources motivating MCMC methods, and describing the relevant algorithms, chiefly Gibbs sampling, Metropolis sampling, and Hybrid Monte-Carlo. When attempting to actually apply these tools, I've come across a few tricks and concepts that weren't clearly signposted in the literature. (The specific problems that required the use of MCMC were [survival curves](https://hilbert-spaess.github.io/STATS-survival-curves/) problems and full parameter inference of neural network models).

## Motivation and intuition

Assume we have a distribution $P(\theta)$ over a high-dimensional vector of parameters $\theta$. We want to get some decent independent samples of $\theta$. Simple approaches like discretizing the parameter space scale badly with increasing dimension. In fact, if the distribution is a posterior distribution on a parameter we're interested in, we hope that the probability is concentrated in a small region of the space. This gives the problem an optimisational flavour- we're looking for the peaks of a complicated probability density function. If we were looking for the point of maximum density, an algorithm like gradient ascent might be useful.

Since we're looking for a sample, and not the maximum a posteriori estimate, we can follow an analagous tactic, by following an 'approximate gradient ascent' that is calibrated to result in a sample. Formally, we follow a Markov chain that tends to a sample from the target distribution. Without going into detail, we assume that this is achieved if the target distribution is invariant under the Markov chain.

----
**Idea:** Carry out a biased random walk around the parameter space. This will be useful for the same reason that gradient descent is useful. Formalised as a Markov chain under which the target distribution is invariant.
----

Again, without getting too fussy about details, there's a simple condition for deciding if 



## Chains-within-chains

## ARS

## Dimension-jumping

## Checking everything's working
