## Causal definitions of incentives

A recent Deepmind [paper](https://arxiv.org/pdf/2001.07118.pdf) gives definitions (in the framework of causal graphical models) for when an agent has an incentive to care about a variable. These definitions are phrased in the language of what the authors call "influence diagrams", which are causal structural models with some special **decision nodes** and **utility nodes**. A utility node is childless and has a value that represents the utility of an agent. A decision node is a node on which interventions are feasible (the agent has the power to carry out intervention on this variable). A **policy** is a specification of the function that determines the decision node given its parents.

We assume a single decision node and a single utility node. Throughout we assume that the agent uses an optimal policy (ie a policy that maximises the expected value of the utility node).

An agent has an **incentive to intervene** on a variable $X$ if there exist circumstances under which an intervention on $X$ has non-zero causal effect on a utility node. This is equivalent to the existence of a front-door path from $X$ to $U$. The authors point out that we only really want to say that there exists such an incentive if an intervention is actually plausible. They therefore decide that the agent has a **control incentive** on $X$ if an intervention to replace $X$ with a potential response to intervention on $D$ has non-zero causal effect on a utility node. (ie, if plausible interventions on $X$ have an effect on utility). This is equivalent to the existence of a front-door path $D \to U$ through $X$. 

An agent has an **incentive to respond** to variable $X$ if an intervention on $X$ has non-zero causal effect on $D$. This is equivalent to a front-door path $X \to D$, and $X$ not d-separated from $D$ by the parents of $D$ that aren't ancestors of $X$. (ie X is relevant to utility, and its relevance isn't entirely mediated by the decision).

These are some simple definitions- I guess it's nice to be able to formalise "X has an incentive to care about affecting Y" and "X has an incentive to care if Y changes". Not quite sure how these got spun out into a whole paper. The "applications" section is also really weird: they basically re-define the non-existence of a reponse incentive to a 'protected variable' (ie something you'll get shouted at if you respond to, like race or gender) as 'counterfactual fairness', and present this re-definition as a theorem.

## Shalizi's causality chapters

## Causation without manipulation?

## Neural networks as a good general regression framework?
