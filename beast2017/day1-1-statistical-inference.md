# Basic principles of statistical inference (Oliver Pybus)
Statistical inference is *not* necessarily
Biological scientists are taught that stats is like a recipe: a plug-and-play thing.

Def: Statistical inference = the use of a data sample to draw inferences about some aspect of the situation from which the data are taken.

The "holy trinity" of statistical inference: data, model and hypothesis.

## Data
 - Strictly speaking, we can't throw out data so that it can fit some model. This is, however, different from ditching data that we know to be wrong.
 - We typically get alignment data, with date and location stamps. Sometimes, we can p'type trait data as well.
 - Population genetic inference usually requires that seqs are approximately randomly sampled - but phylo inference often don't require random sampling (note that theoretically, even the concept of "random sampling" isn't very rigorously defined)
 - Data is assumed to be correct, but uncertainty in the data can often be modelled/represented, e.g. ambiguity codes for nucleotides.
 - Alignment uncertainty is usually ignored.

Open question - is the tree structure a model or a parameter (state) within a broader class of all possible trees?

## Hypothesis
 - A theory of the situation under study.
 - Mathematically, a hypothesis is some statement about the **parameter values of the model**
 - The data can then be used to assess whether the given hypothesis is correct or note
 - The model may have many params, but the hypothesis may not concern all of them.  The rest are called *nuisance params*.

## Goals of inference*
*Point estimation* - using the data to estimate values for one or more model params. e.g."When was the TMRCA of my sampled sequences?"
 - Data: sequence alignment, dates of sampling, tree topology (treated as fixed. But we could also make topology a nuisance parameter).
 - Model: HKY
 - Estimated params: age of root nucleotides
 - nuisance params: ages of the other nodes in the tree (e.g. branch lengths)
*Interval estimation*
Using the data to provide a range which represents the degree of uncertainty in the estimate of a parameter. E.g. "what are the 95% CIs for the evolutionary rate of my sequences?"
*Hypothesis testing*
Using the data to assess the relative plausibility of different statements about model params. e.g.
- "is my estimate dN/dS significantly >1?"
- Does REV fit my data better than HKY?
- Can I reject a strict molecular clock?
*Model selection*
 - Find the most appropriate model for your data
 - Involves a tradeoff between "goodness of fit" and predictive power (i.e. bias-variance tradeoff). Adding params increases the former but decreases the latter. Note that we're better able to do this analytically if the models belong to the same family space (e.g. polynomial functions). This is not quite possible for tree space.
 - But even the best-fitting data can explain the data poorly!
 - Practical example: Jukes-Cantor, or GTR GAMMA?

## Segway:
 - A **tree** consists of only two elements: the ordering of splitting, and branch lengths.
 - Note that all possible trees for a given dataset have the *same number of paramsters*, so finding the "best tree" in some sense is purely an issue of goodness-of-fit.

## Inference Frameworks
 - Several diff kinds of statistical Inference
 - Evolutionary problems often involve complex models with many params, and sometimes limited amounts of data.
 - Likelihood (viz. frequentist) and Bayesian inference are practically much the same, but philosophically different.

*Likelihood (frequentist)* - probabilities refer only to the outcome of experiments, representing frequencies of outcomes if the experiment were repeated many times. The degree to which data supports a hypothesis is the likelihood.

*Bayesian inference* - Both data and model params are described by probabilities. Probabilities reflect our degree of belief in a hypothesis, as well as representing the outcome of experiments. Hence, hypotheses have probabilities even in the absence of data.
 - *hard school*: prior knowledge (probabilities) comes from previous knowledge of the system
 - *soft school*: we haven't rolled that dice at all, but we generally know that dice are pretty fair (uniform prior). So that seems like a logically defensible starting position.
Note that Bayesian inference forces people be explicit about their assumptions (priors), which is a good thing. Don't get too bogged down by semantics of "belief" or "prior knowledge", because that's a philosophical rabbit hole from which you'll never emerge.

## Properties of Inference Frameworks
*bias* - the average deviation of an estimate from the true value
*variance* - spread of values from the true value
*consistency* - convergence of an estimate to the true value as sample size increases
*Likelihood* - a technique for assessing the relative merits of different hypotheses in the light of the data.
P(D|H) = probability of observing the data D, given hypothesis H.
The likelihood of hypothesis H, given data D, is denoted P(H|D). Most importantly:

P(D|H) is proportional to L(H|D).  I don't quite get this, because this is a pretty strong arithmetic claim that seems to have come out of nowhere.

- Inferences are made by comparing the likelihoods of different hypotheses on the same data D.
- **Never compare likelihoods on different data!**

## MLE
- Suppose we have a model with one parameter, x
- We'd like to find the value of x which maximizes the likelihood. This is the MLE of x. We can use algebra, or find this by optimization algorithms.

## Likelihood Ratio
 - Likelihood ratio statistic = 2 * (max(L(H1|D)) - max(L(H2|D)))
 - Only works if the hypotheses are nested (i.e. one is a special case of the other, e.g. exponential vs. gamma).
 - LRS can also be used to compare their GoF, and calculate CIs for MLEs.

## Akaike IC
Non-nested hypotheses can be compared using AIC.
"Better" hypotheses would have higher AIC values.

## Bayesian Inferences
 - spits out a posterior probability distribution rather than a likelihood curve.
 - This "posterior" combines info from the data and from previous (prior) knowledge (likelihood returns information from the data only)
 - Each parameter in the model has a prior df representing our previous knowledge or belief about the parameter.
 - The prior can be "strong" or "weak". Strong: "human heights ~N(1.7m, 0.1cm)". Weak: "human heights~U(10E-3mm, 10km)"
Alexei Drummond: when in doubt, you can get away with using a weak prior, because MCMC will converge after enough iterations.
 - If the posterior and the prior look similar, then the data is not very informative about the parameter in question. So either you've chosen the wrong prior (or you've estimated the data perfectly!).

## Approximating posterior with MCMC
 - Walks around param space in a pseudo-random way, moving through "low probability" regions fast and slowly in "high probability" regions. Params are estimated by finding the mean or median of the posterior - these are the *Bayesian posterior estimates*.
 - HPD - the smallest region that contains 95% of the posterior probability. The Bayesian analogue to a CI.
 - The Bayesian equivalent of the LRS if the "Bayes factor", Bayesian inference in general sucks at model selection:

 BF = P(D|Model1) / P(D|Model2)

Models 1 and 2 need not be nested.
M1 and M2 can represent different models, or different regions of parameter space.
It's really hard to compute BF!

Bayes factor < 1: M1 is worse than M2.
3 - 10: substantial support for M1
> 10: good support for M1
> 100: extremely good supprot for M1
