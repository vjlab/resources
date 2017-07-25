# Setting Priors and Initial Values (Stephane)
## What is a prior?
- Df of a param before the data are collected and analyzed
- Allows us to include any background information we have, using results of independent experiments, or other independent evidence.
- The prior df does not have to, and is not expected to, be exactly the same as the posterior.
- Not universal, but data specific
- Should not be too restrictive if prior assumptions are weak.
- Do *not* adjust after a run to give higher posterior support.

## Nuc Sub model prior
- Favour a model that worked previously.
- Use JModel test, or rjMCMC in BEAST2 to sample from the posterior including different substitution models. The model where rjMCMC spends the most time (gets the most samples from) is the best fitting model.

## Clock Prior (Molecular Clock Model)
- Strict clock: all branches have the same substitution rate
- Relaxed model: Allows sub rates to vary along diff branches.
  - Uncorr - branches have idp't clock rate distributions
  - corr - child branch has clock rate distribution correlated to distribution of parent branch.

## Param priors
- can be fixed to a given value (not recommended)
- Can ~U(upper, lower). A uniform prior is not exactly an uninformative prior because you'd still have to specify upper and lower bounds. Avoid uniform priors across an infinite domain.
- If little or no information is available, use diffuse priors.
- Can be set as a parametric distribution, with its own params (hyperprior)
- Distributions are visualized in BEAUTi
- Try "sampling from the prior" to get a better idea of which prior to choose.

## Words of Caution
- Evaluate the impact of a prior on the posterior in the Bayesian robustness analysis
- Ideally, the posterior should be dominated by your data, such that the choice of the prior has little influence on the result.
- If this is not the case, the choice of prior is very important, and should be reported.
- If prior = posterior, then the data isn't adding any information at all, and you might as well not use the data. (Oliver: and Bayes Factor will be maximal)
