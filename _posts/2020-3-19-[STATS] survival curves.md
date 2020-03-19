**Summary**

- If you want to model survival data, you can make a massive Bayesian survival curve model, and do inference on the parameters.
- You can model the time until death (for a specific cause) with an exponential distribution, a gamma distribution, a Weibull distribution, or some combination of these. 
- Anything involving the human body (eg death due to some disease) is probably not simple enough to be modelled with a single distribution. You could model it as due to some mixture of independent causes, each occurring with some probability.

TODO: -> compare some samples from priors for single gamma and gamma mixture.

**Survival Analysis**  

The canonical example of survival analysis is understanding the death timeline of patients with a life-threatening disease. It's a special case of the more general problem of figuring out the expected period of time before the occurrence of some event. Other examples are the relapse of an addict or the failure of some mechanical system. The two examples I've looked at myself are the occurences of deaths in MTB patients, and the incubation period of the new coronavirus. From now on I'll use the language of the death example.

**The functions we're trying to understand**

Suppose we have patients who test positive for some disease. Let $T$ be the variable denoting time of death. The *survival curve* or *survival function* is $S(t) = \mathbb{P}(T > t)$. If the probability of eventual death is $p$, this looks like a function decreasing from 1 and approaching $p$ asymptotically.

The *death rate* or *event density* is the rate of death (in expectation) per unit time. Given that $1 - S(t)$ is the cumulative probability of death, we may compute it as $f(t) = (1 - S(t))' = -S'(t)$. The *hazard function* $\lambda(t)$ (or *hazard rate*, or *force of mortality*) is the death rate at time $t$, conditioning on survival up until this point. $\lambda(t) = \frac{f(t)}{S(t)} = \frac{-S'(t)}{S(t)}$. It's roughly "how scared" you should be at time $t$.

The data available for fitting these functions often looks like a vector of death times, sometimes with uncertainty (censored data). The precise time of death might be unknown, as the last observation was made while the patient was still alive.

**Relevant distributions**

The *Exponential distribution*, $f(t)$, and $f(t \vert \lambda) \propto e^{-\lambda t}$. If this is the death rate, the condition has a constant hazard function. (ie death could occur at any time with rate $\lambda$ ). This works as a model for death by meteor strike or spontaneous combustion or something.

The *Gamma distribution* is a more flexible two-parameter generalisation of an exponential distribution, also useful as the conjugate prior for an exponential distribution. Another reason to care about it in this context is that it's the distribution of a sum of a set of exponential variables, which could models a death that occurs after several stages of ailment, each with exponential lifetime. The distribution is $\Gamma(t \vert m, r) \propto t^{m-1} e^{-rt}$. The parameters $m$ and $r$ are the 'shape' and 'rate' respectively. The exact density function: $\Gamma(t \vert m,r) = \frac{r^m}{\Gamma(m)}t^{m-1}e^{-rt}$ When $m=1$, the distribution is exponential and the hazard function is constant. When $m > 1$, the hazard function is concave and increasing, and when $m < 1$, the hazard function is convex and decreasing. 

The *Weibull distribution* also gives increasing or decreasing hazard functions, and is also a generalisation of the exponential distribution. $W(t \vert \lambda, p) \propto t^{p-1} e^{-(t/\lambda)^p}$, where $\lambda > 0$ is scale, and $p > 0$ is shape. A Weibull death rate gives rise to a hazard function that is proportional to a power of time. If $p < 1$, the hazard rate decreases over time. If $p = 1$, the distribution is exponential and hazard rate is constant. If $p > 1$, failure rate is constant.

Apparently the *log-logistic distribution* might be useful as well, but I don't know what it is.

**A Bayesian Model**
(shown to me by Roger Sewell)

Suppose we are working with a dataset of times until death, some values of which have been right-censored (ie we know the last time at which the patient was guaranteed to be alive, but we have no information about the time of death). We want to completely model the survival curve of the condition. 

We assume that death is due to some number of independent causes, each affecting a patient with a fixed probability. We model each cause of death with a Gamma distribution, with an extra parameter added to incorporate Weibull-like increasing or decreasing hazard functions. Implicitly here we're modelling each cause of death as a chain of independent failures, each of which has exponential lifetime, and each with an overall increase or decrease in likelihood as time goes on.

Now we can make the above precise. Let $J \geq 0$ be the number of causes of death. We can put a geometric prior on $J$. For each cause of death $j$, let $x_j$ be the vector of times at which $j$ would have killed each patient. (Possibly some entries of $x_j$ are $\infty$ ). Let $x = \min_{1 \leq j \leq J}x_j$ denote the time of death of each patient. Since the data might be censored, we will have to do inference on $x$ itself. Dropping the subscript $j$ (and assuming that what follows will be repeated for each cause of death), we assume that every entry in $x$ is distributed according to $P(x \vert p, k, m, r)$, meaning that with probability $p$, $x^k$ is Gamma distributed with parameters $m' = m$ and $r' = mr^k$, and otherwise $x  = \infty$. (ie with probability $p$ the cause of death pertains, and has parameters $m, r, k$ ). We use sensible conjugate priors for $p, k, m, r$. 

**Carrying 
             * Specifically, $P(y|p,k,m,r,u) = 
             * Assign conjugate priors to all parameters $p, k, m, r$.
         * Given censored death data, we perform inference on $J, x, p, k, m, r$ simultaneously.
     * Carrying out inference with this model
         * MCMC, in particular Gibbs sampling, suffices to get good samples from the posterior.

** Comparing the model
