<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Previous posts on causal inference [here](https://hilbert-spaess.github.io/stats-Causality-from-correlation-Pearl's-approach/), [here](https://hilbert-spaess.github.io/Simpsons's-Paradox-and-computing-causal-effect/), and [here](https://hilbert-spaess.github.io/Confusions-about-causal-inference/).

## Causal definitions of incentives

A recent Deepmind [paper](https://arxiv.org/pdf/2001.07118.pdf) gives definitions (in the framework of causal graphical models) for when an agent has an incentive to care about a variable. These definitions are phrased in the language of what the authors call "influence diagrams", which are causal structural models with some special **decision nodes** and **utility nodes**. A utility node is childless and has a value that represents the utility of an agent. A decision node is a node on which interventions are feasible (the agent has the power to carry out intervention on this variable). A **policy** is a specification of the function that determines the decision node given its parents.

We assume a single decision node and a single utility node. Throughout we assume that the agent uses an optimal policy (ie a policy that maximises the expected value of the utility node).

An agent has an **incentive to intervene** on a variable $X$ if there exist circumstances under which an intervention on $X$ has non-zero causal effect on a utility node. This is equivalent to the existence of a front-door path from $X$ to $U$. The authors point out that we only really want to say that there exists such an incentive if an intervention is actually plausible. They therefore decide that the agent has a **control incentive** on $X$ if an intervention to replace $X$ with a potential response to intervention on $D$ has non-zero causal effect on a utility node. (ie, if plausible interventions on $X$ have an effect on utility). This is equivalent to the existence of a front-door path $D \to U$ through $X$. 

An agent has an **incentive to respond** to variable $X$ if an intervention on $X$ has non-zero causal effect on $D$. This is equivalent to a front-door path $X \to D$, and $X$ not d-separated from $D$ by the parents of $D$ that aren't ancestors of $X$. (ie X is relevant to utility, and its relevance isn't entirely mediated by the decision).

These are some simple definitions- I guess it's nice to be able to formalise "X has an incentive to care about affecting Y" and "X has an incentive to care if Y changes". Not quite sure how these got spun out into a whole paper. The "applications" section is also really weird: they basically relabel the non-existence of a reponse incentive to a 'protected variable' (ie something you'll get shouted at if you respond to, like race or gender) as 'counterfactual fairness', and present this re-definition as a theorem.

## Shalizi's causality chapters

I had a really quick look at the chapters on causal inference in Shalizi's [statistics textbook](https://www.stat.cmu.edu/~cshalizi/ADAfaEPoV/ADAfaEPoV.pdf), to see if I'd missed anything from Pearl's book. Some similarly quick thoughts:

He uses the causal graphical model framework, which is reassuring. The first chapter, "Graphical Causal Models",  summarises this stuff.

The second chapter covers identifying causal effects from causal structures. Without going into interventional calculus or necessary conditions, it focusses on the back-door criterion and front-door criterion. I'm pretty confused about identifying causal effect with so-called 'instrumental variables', as it looks like we have to make assumptions about the functional form of the causal structure to actually identify causal effect.

The third chapter is a useful complement to Pearl- whereas Pearl assumes direct access to observable distributions, Shalizi points out that estimating the relevant conditional distributions is a regression problem. If we aren't conditioning on too many variables, and the distributions are discrete, we should be able to just do inference, like in the first point [here](https://hilbert-spaess.github.io/Confusions-about-causal-inference/). Another non-parametric approach that Shalizi suggests is nearest-neighour smoothing, or 'matching'. Otherwise we have to whip out the regression toolbox.

## Causation without manipulation?

## Neural networks as a good general regression framework?
