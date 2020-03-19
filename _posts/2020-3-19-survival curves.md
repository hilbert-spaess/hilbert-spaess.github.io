* Overview of the problem
     * Problem description
         * Canonical application: want to understand the expected timeline of death of patients with a severe disease.
         * In general, want to understand the expected period of time before the occurrence of some event. Typically death or failure of some sort. In what follows, will use the language pertaining to death.
         * Two examples I've worked with so far:
             * Estimating expected lifetime for MTB patients, given death data with some censoring.
             * Estimating incubation period of infectious disease, with uncertain time of infection.
         * Applications that seem interesting, but I haven't looked at
             * survival curves for different species of wild animal.
             * survival curves for soldiers in different wars.
     * Functions to be estimated:
         * Let $T$ be the time of death. The *survival curve* or *survival function* is $S(t) = \mathbb{P}(T > t)$. If the probability of eventual death is $p$, this looks like a curve decreasing from 1 and approaching $p$ asymptotically.
         * The **death rate** (or **event density**)  is the rate of deaths per unit time. Given that $1 - S(t)$ is the cumulative probability of death, we may compute  It is computed as $f(t) = (1 - S(t))' = -S'(t)$.
         * The **hazard function** (or **hazard rate** or **force of mortality**) is the event density at time $t$, conditioning on survival until time $t$. This is $\lambda(t) = \frac{f(t)}{S(t)} = \frac{-S'(t)}{S(t)}$. Roughly speaking, it's "how scared" you should be at time $t$.
             * Whereas the survival curve decreases monotonically, you can get more interesting shapes from the hazard function.
     * Data available:
         * Most often, data is available as a vector of times of death $t$. So the problem looks something like "fitting a survival curve" to the observed points.
         * We often get data **censoring**, when not all data is available. For **right-censored** data, the exact time of death is not known. This might happen if the last observation was made before death. For **left-censored** data, the time of onset is important and unknown.
 * Relevant distributions
     * Exponential distribution
         * $\textrm{Exp}(t | \lambda) \propto e^{-\lambda t}$.
         * This turns up as the event density for a condition with a constant hazard function. (ie death could occur at any time with rate $\lambda$ ). Not many human diseases have constant hazard functions, but it's a good model for radioactive decay.
     * Gamma distribution
         * More flexible generalisation of an exponential distribution, also useful as the conjugate prior for an exponential distribution. It is also the form of the sum of a set of exponential variables, which models a final failure that occurs after several stages of failing with exponential lifetime.
         * $\Gamma(t | m, r) \propto t^{m-1} e^{-rt}$. The parameters $m$ and $r$ are the 'shape' and 'rate' respectively.
         * Precise density function: $\Gamma(t | m,r) = \frac{r^m}{\Gamma(m)}t^{m-1}e^{-rt}$
         * When $m=1$, the distribution is exponential and the hazard function is constant. When $m > 1$, the hazard function is concave and increasing, and when $m < 1$, the hazard function is convex and decreasing. 
     * Weibull distribution
         * The Weibull distribution also gives increasing or decreasing hazard functions, and is also a generalisation of the exponential distribution.
         * $W(t | \lambda, p) \propto t^{p-1} e^{-(t/\lambda)^p}$, where $\lambda > 0$ is scale, and $p > 0$ is shape.
         * A Weibull survival curve gives rise to a hazard function that is proportional to a power of time. If $p < 1$, the hazard rate decreases over time. If $p = 1$, the distribution is exponential and hazard rate is constant. If $p > 1$, failure rate is constant.
     * Log-logistic distribution
 * Flexible Bayesian model shown to me
   (by Roger Sewell)
     * Specification of the model
         * We are working with right-censored death data (ie, for some patients only a lower bound on time of death is known). We want to work with a full model
         * We assume that there are a number of potential causes of death, each occurring with some probability. Use a Gamma distribution for each cause of death, with an extra parameter to incorporate Weibull-like increasing or decreasing hazard functions. We now consider the parameters of the model in turn.
         * Let $J$ be the number of causes of death. $j \in \{1, ..., J\}$ will denote a particular cause of death.
             * Geometric prior on $J$ is sensible.
         * For each cause of death $j$, let $x_j$ be the vector of times at which  $j$ would have killed each patient. (Possibly some entries of $x_j$ are $\infty$ ).
         * Let $x = \min_{1 \leq j \leq J}x_j$ denote the time of death of each patient.
         * Dropping subscript $j$, and considering a single patient $x$, we assume that $x$ is distributed according to $P(x | p, k, m, r)$, meaning that with probability $p$, $x^k$ is Gamma distributed with parameters $m' = m$ and $r' = mr^k$, and otherwise $x  = \infty$.
             * Specifically, $P(y|p,k,m,r,u) = 
             * Assign conjugate priors to all parameters $p, k, m, r$.
         * Given censored death data, we perform inference on $J, x, p, k, m, r$ simultaneously.
     * Carrying out inference with this model
         * MCMC, in particular Gibbs sampling, suffices to get good samples from the posterior.
 * Alternative models
     * 
