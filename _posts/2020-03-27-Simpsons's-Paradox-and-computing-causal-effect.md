<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is a follow-up to my [previous summary](https://hilbert-spaess.github.io/stats-Causality-from-correlation-Pearl's-approach/) of causal inference with graphical causal models. Simpson's paradox is a phenomenon in which a correlation reverses once a new confounding variable is taken into account. Any 'paradoxical' conclusions can explained using causal inference. This problem leads naturally to the consideration of general strategies for computing causal effect.

## Medical Trials

Suppose we are comparing two treatments for a disease. Suppose the disease has two severity levels, and everyone who catches it either dies or is cured. In other words, suppose we have an observed distribution over three binary variables. The following are some imaginary data (showing the fraction of observed patients with a positive outcome $O$): 

| | **Treatment T = 1** | **Treatment T = 2** | 
|**Severity S = Low**| 18/20 | 71/103
|**Severity S = High**| 32/105 | 3/40
|**Total** | 50/125 | 74/143

When aggregated, Treatment 2 is more likely to save lives than treatment 1. However, considering each severity level separately, in both cases Treatment 1 is preferable. The surprising conclusion is that taking into account an extra variable reverses the trend that might be extrapolated from the total figures. So if you were a patient, which treatment would you want to take?

Let's be precise about what conclusions there are to be drawn from the dataset. The last row gives us estimates for $P(O \vert T)$: the probability of good outcome, given the treatment chosen. This is a conditional probability, *not an interventional probability*. It's very different from the probability of a good outcome given that we step into the causal structure and artificially fix the choice of treatment. In this case, part of the reason that the outcome is better for patients taking treament 2 is that patients undergoing this treatment were more likely to have a low-severity case in the first place. To actually talk about the interventional probability $P(O \vert \hat{T})$, we need to explicitly consider the causal structure. Here are some candidates:

![t-o](/images/t-o.jpg) | ![t-o-s-vee](/images/t-o-s-vee.jpg) | ![triangle-tso.jpg](/images/triangle-tso.jpg)
Structure 1 | Structure 2 | Structure 3

Severity and outcome are not independent, so the first causal structure doesn't work. As noted above, treatment and severity are not independent, so the second structure won't work. The third structure is compatible with the distribution. For this to be the correct causal structure we need to assume that no variables other than severity and treatment will have a causal influence on outcome. Now an intervention on the value of the treatment variable changds the structure to that in diagram 2. So $P(O \vert \hat{T}) = \sum_{S}P(S)P(O \vert T, S)$

The total figures correspond to looking at the conditional probabilities $P(O \vert T)$.
Averaging over the severity levels corresponds to looking at $\sum_{S}P(S)P(O \vert T, S) = P(O \vert \hat{T})$. Summing over marginal probability of severity levels and conditioning in this fashion is termed "adjusting for severity". In this case, adjusting for severity is equivalent to computing causal effect.

As a patient looking to maximise our chances of recovery, the interventional probability is what is interesting, so the trend observed by adjusting for severity level is what is relevant to our choice. Hence we should choose the first treatment.

## Computing causal effect with unobserved variables.

The general problem suggested by Simpson's paradox is working out when we have enough information about the causal structure $G$ to compute the causal effect of one variable on another. In the above example we needed the relatively strong assumption that there were no latent variables affecting outcome (ie that the model was Markovian). Then we knew the whole structure $G$, so it was easy to compute the effects of interventions. But what can we do with weaker assumptions? To start with, let's consider what happens in the case that we know the causal structure among the observed variables, but there could be unconsidered latent variables. This was essentially the case with the medical example above, but without the unrealistic assumption that we knew all relevant variables.

Once latent variables are a possibility, we can't always compute causal effect. As explained previously, we can assume all latent variables are common causes of precisely two observed variables, and as shorthand for the potential presence of these unobserved latent causes we use bidirectional *confounding arcs*. Here are some examples of causal structures over observed variables in which the causal effect of the red variable on the blue can't necessarily be found: 

(x -> y) (x -> y z triangle)

Pearl derives a set of manipulation rules for expressions involving actions and observations, referring to semi-Markovian models. If we can reduce an expression involving actions to an expression purely referring to distributions over the observed variables, we've computed the causal effect. Before we had essentially one manipulation rule, the reduction of conditional independence to d-separation. This can be summarised as a condition under which we can remove conditioning on an observation. Now that we can condition on observations and actions, there are three manipulation rules, governing the removal of an observation, the removal of an action, and the swapping of an action and observation.

**Notation:** Let $G$ be a DAG associated with a Markovian causal model, and let $P$ be the induced probability distribution. Let $X, Y, Z$ be arbitrary disjoint subsets of vertices in $G$. Then we denote by $G_{\bar{X}}$ the graph obtained by deleting all arrows into vertices in $X$. This is the causal structure after intervening on the value of $X$. Likewise, we denote by $G_{\underset{\bar{}}{X}}$ the graph obtained by deleting all arrows out of vertices in $X$. 

**Rule 1: (deletion of observation)** $P(Y \vert \hat{X}, Z, W) = P(Y \vert \hat{X}, W)$ if $(Y \perp_{G_{\bar{X}}} Z \vert X, W)$. 

This rule states that d-separation in the mutilated graph is still sufficient for conditional independence after taking an action. This follows from the fact that removing edges cannot induce dependencies.

**Rule 2: (action <-> observation)** $P(Y \vert \hat{X}, \hat{Z}, W) = P(Y \vert \hat{X}, Z, W)$ if $(Y \perp_{G_{\bar{X} \underset{\bar{}}{Z}}} Z \vert X, W)$.

This provides a condition under which we can replace an intervention probability with an observation probability. The effect of an intervention on $Z$ is the same thing as conditioning on $Z$ only if the only way $Z$ affects $Y$ is through its descendants. This happens iff $X \cup W$ d-separates $Y$ and $Z$ in $G_{\underset{\bar{}}{Z}}$.

**Rule 3: (deletion of actions)** $P(Y \vert \hat{X}, \hat{Z}, W) = P(Y \vert \hat{X}, W)$ if $(Y \perp_{G_{\bar{X} \bar{Z(W)}}} Z \vert X, W)$, where $Z(W)$ is the set of Z-nodes that are not ancestors of any W-node in $G_{\bar{X}}$.

Condition under which we can remove an action. Require that the action have no effect on $Y$ via its ancestors. The reason for deleting only non-W-ancestors is not obvious to me yet.

Using these three rules, we can sometimes express causal effects in terms of the observed distributions, even when workng in a model with confounding arcs. There exists a sufficient condition for being able to compute the causal effect:

**Theorem:** (Pearl, Tian, 2002) A sufficient condition for being able to compute the causal effect $P(Y \vert \hat{X})$ is that there exists no path composed of confounding arcs between $X$ and any of its children in the graph obtained by deleting non-ancestors of $Y$ from $G$.

Applying this criterion, we see why the causal effect of green on blue can be computed in the on the left-hand-side below, but not on the right. (The white nodes in the DAGs are the unobserved confounding latents).

![criterion example](/images/criterion_g_b.jpg)

Tian and Shpitser give a summary of the latest necessary and sufficient conditions [here](http://web.cs.iastate.edu/~jtian/papers/tian-shpitser-2009.pdf) (the problem is essentially solved as far as I can tell, with polynomial time algorithms for determining whether arbitrary quantities involving actions can be computed in semi-Markovian models).

## Lung Cancer example

The above left-hand structure turns up a lot, and is a classic example of the power of identifying causal effects. The example here will take us right back to Simpson's paradox, resolved with a different underlying structure, and with weaker assumptions. 




