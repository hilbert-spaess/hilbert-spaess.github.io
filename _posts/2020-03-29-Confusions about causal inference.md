Some things I'm confused about / that need resolving. This is in the context of my previous posts on causal inference: [here](https://hilbert-spaess.github.io/stats-Causality-from-correlation-Pearl's-approach/) and [here](https://hilbert-spaess.github.io/Simpsons's-Paradox-and-computing-causal-effect/).

## Extracting conditional independence sets from data.

**Confusion**: Pearl's approach centres on the ability to take samples from a distribution and determine conditional independencies. He assumes that we have access to the distribution itself, which renders the problem trivial. It reality, it doesn't seem that obvious.

The problem of recognising conditional independencies of discrete random variables boils down to deciding whether samples have been taken from the same discrete distribution. This can be solved by comparing the likelihoods of two different models. We can take a Dirichlet prior over all multinomial distributions, and compare the model in which the two distributions are equal and sampled from the prior, and a model in which they are sampled independently. Computing the log-likelihood ratio can inform our decision as to whether the variables are conditionally independent, or whether we need to gather more samples.

(Example with binary random variables).

Complexity of algorithm for finding the independencies?

## Why minimality is sensible (as opposed to some prior)

**Confusion:** Pearl seems to favour a strong form of Occam's Razor: discard any models that aren't minimal. I would have expected an approach that takes some sort of complexity prior over causal structures.

First thought: if one structure dominates another, then under any sensible metric over possible models, the models of the dominated structure have measure 0 as a subset of the larger structure. So it makes sense to flat-out reject any model if it strictly dominates another model.

Second thought: but why can't I use this to say that, eg you should prefer quadratic models to cubic models?

Third thought: oh, Pearl assumes that we have access to the **exact** distribution. So we know that the model fits precisely. In this case, you have to reject the more complex model. If all of your datapoints lie precisely on a quadratic, why postulate a cubic?

So the first two confusions are related, and if we assume we don't have access to the distribution itself, but just samples, we could do inference over model sizes *and* conditional independencies simultaneously. Pearl just prefers a discrete approach, in which we know the distribution precisely, which is easy to theorise about. Conjecture: for most basic diagrams you can spot conditional independency 'by eye' and take minimal models like Pearl.

## Where do considerations of time come into causal inference?

**Confusion:** Vague confusion. Time seems important for reasoning about causality. But Pearl's conclusions refer only to observed variables. Is it possible for $X$ have causal influence on $Y$ in the sense of Pearl, but come later in time? Otherwise, where does time come in?

It turns out that Pearl also writes about this. He notes that humans expect causal relations to satisfy the statistical constraints he's presented, but also to satify the basic temporal constraint that the cause precedes the effect. So there's a *temporal bias*, where we only see certain patterns of dependencies between events in time. For example, present events can render future events conditionally independent, but we rarely see a present event rendering past events independent.


## Continuous vs discrete variables

**Confusion:** What do causal models with continuous variables look like? 

In general, it's hard to test for conditional independence of continuous random variables. (To do a model comparison like that outlined above would require a prior over continuous distributions, which isn't going to happen). This is why a fully general model with continuous variables is unlikely to be practical. If the variable in question is in reality continuous, we can use discrete bins and retain independence structure. If we constrain the models to certain form (eg variables are noisy linear functions of their parents), then we should be able to do inference with continuous observed variables. (See Gelman's stuff and Rubin's stuff).

## What are some real-world examples of applications of graphical causal models?

## Where does carrying out experiments fit into Pearl's model of observational causal inference?

## Good/True intuitions (link) for the various conditions + criteria.
