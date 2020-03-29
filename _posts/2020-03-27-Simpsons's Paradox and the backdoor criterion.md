<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ['\\(','\\)']], processEscapes: true } }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

This is a follow-up to my [previous summary](https://hilbert-spaess.github.io/stats-Causality-from-correlation-Pearl's-approach/) of causal inference with graphical causal models. Simpson's paradox is a phenomenon in which a correlation reverses once a new confounding variable is taken into account. Any 'paradoxical' conclusions can explained using causal inference. 

## Medical Trials

Suppose we are comparing two treatments for a disease. Suppose the disease has two severity levels, and everyone who catches it either dies or is cured. In other words, suppose we have an observed distribution over three binary variables. The following are some imaginary data (showing the fraction of observed patients with a positive outcome $O$: 

| | **Treatment T = 1** | **Treatment T = 2**
|**Risk R = Low**| 18/20 | 71/103
|**Risk H = High**| 32/105 | 3/40
|**Total** | 50/125 | 74/143

When aggregated, Treatment 2 is more likely to save lives than treatment 1. However, in both low risk and high risk circumstances, Treatment 1 is preferable. The surprising conclusion is that taking into account an extra variable reverses the trend that might be extrapolated from the total figures. So if you were a patient, which treatment would you want to take?

Let's be precise about what conclusions there are to be drawn from the dataset. The last row gives us estimates for $P(O \vert T)$: the probability of good outcome, given the treatment chosen. This is a conditional probability, *not an interventional probability*. It's very different from the probability of a good outcome given that we step into the causal structure and artificially fix the choice of treatment. Indeed, one reason for this is given by the table: it looks like many more low-risk patients are prescribed with treatment 2. To actually talk about $P(O \vert \hat{T})$, we need to explicitly consider the causal structure. Here are some candidates:

![t-o](/images/t-o.jpg) | ![t-o-s-vee](/images/t-o-s-vee.jpg)
Structure 1 | Structure 2 

Risk 