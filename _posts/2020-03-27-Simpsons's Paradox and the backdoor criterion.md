This is a follow-up to my [previous summary](https://hilbert-spaess.github.io/stats-Causality-from-correlation-Pearl's-approach/) of causal inference with graphical causal models. Simpson's paradox is a phenomenon in which a correlation 'reverses' once a new confounding variable is taken into account. Any 'paradoxical' conclusions can explained using causal inference.

## Medical Trials

Suppose we are comparing two treatments for a disease. Suppose the disease has two severity levels, and everyone who catches it either dies or is cured. In other words, suppose we have an observed distribution over three binary variables. The following are some imaginary data: 

| | **Treatment 1** | **Treatment 2**
|**Low risk**| a | b
|**High Risk**| c | d
|**Total** | e | f

When aggregated, Treatment 2 is more likely to save lives than treatment 1. However, in both low risk and high risk circumstances, Treatment 1 is preferable. The surprising conclusion is that taking into account an extra variable reverses the conclusion that might be drawn by looking at only the total figures.

Let's be precise about what conclusions there are to be drawn from the dataset. The last row gives us estimates for $P(\textnormal{Outcome} \vert \textnormal{Treatment})$. 
