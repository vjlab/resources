# How to BEAST (Louis du Plessis)
1. Build-a-BEAST model
2. Crash course in MCMC
3. BEAST2 workflow

Bayes' Thm:
P(M|D) = P(D|M)P(M)/P(D)

We don't care about P(D).

Base data structure in BEAST is a rooted-time tree.

## What can go into a BEAST model?
1. Genetic sequences - duh.
2. Genealogy - what are the ancestral relationships between the sequences in our datasets?
3. demographic model - describes how the tree grows over time, P(tree|demographic model)). Diff population dynamics generate different trees. Usually coalescent or birth-death. Coalescent (goes backwards in time)- assumes Wright-Fisher-like population dynamics, given effective pop size (N_e). Birth-death (goes forward in time). Lambda = infection rate, delta = becoming non-infectious rate, p = sampling probability.
4. site model - how sequences evolve along the tree. We observe sequences at their tips, not their histories. Assumes every site evolves independently, and substitutions are Markovian. See Chapman-Kolmogorov thm, for interest. Note: K80 (transition/transversion) always eventually converges on a uniform distribution of nucleotides. Also does not have a symmetric state transition matrix.

Gamma-distributed rate variation is not flexible enough to model differences between different loci. Use a separate substitution model (partitions)
5. Molecular clock model - dates the tree. Scales branch lengths to calendar time. Different branches may have different clock rates. Priors on different internal nodes can help to calibrate the clock.

Note that these 5 choices are not really independent of each other!

### Exceptions
 - site models don't have to be on nuc data - we can also use aa data, morphological traits, roots of words, etc.
 - BEAST2 doesn't always use trees!

# How does BEAST compute the Posterior (spoiler: MCMC)
 - MCMC performs a random walk on the posterior, preferentially sampling high-density areas
 - draws samples from the posterior, outputs a list of values that can approximate the posterior
 - We need only compare which posterior density is higher, so we only need the ratio of posterior
 - Alexei: if we leave this to run forever, the random walk would eventually explore everywhere.
 - Alexei: MCMC runs so that the equilibrium distribution == the posterior distribution.

 How good is an approximation?
  - If we knew what the posterior was, then we'd want approximately q% of points inside q% of contours ("contours" are like "percentiles").

*Target distribution* - this is the posterior in BEAST2. MCMC steps through param state space and samples the target distribution.
*proposal distribution* - used to decide where to step to next. This choice only affects the efficiency of the algorithm.
*Operators* - part of the MCMC algo, not the proposal df.

*Input* - MCMC chain length, and interval (how often to record samples so that they're not correlated). >10,000 MCMC samples is a waste of space; the trick is to sample at the right frequency.
*After* - discard burn-in, assess convergence and mixing. Is the chain **mixing** well? (i.e. does it look like a nice caterpillar? Should look like white noise, i.e. uncorrelated.) Are samples uniformly drawn from all over the stationary distribution? The MCMC algo might be getting stuck in a hill, then making a jump to another hill.

*Protip* - do multiple runs, and see if they converge on the same posterior.
 - the posterior may be bimodal, or not a nice bell shape!

## BEAST Best Practices
(Only a guideline; each analysis is unique)
 - Know thy data, to plan the five different inputs.
 - Run analysis with multiple chains. Combine chains, assess convergence and autocorrelation.
