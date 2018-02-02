# Selection Analysis with `HyPhy`

This tutorial covers using my Python3 `wrapomatic` wrapper for these two methods (more incoming when I find the time!). `wrapomatic` was built around HYPHY 2.3.720180108beta(MP). IF you already have it installed, use `$ HYPHYMP -v` to check which version you've got. New 2.3.x versions seem to come out at least once a month with single bug fixes, so this wrapper *should* (fingers-crossed) work with any 2.3.x version. 

## Installation

Follow the [installation instructions](https://veg.github.io/hyphy-site/installation/) on their website. Somewhat long, but should be straightforward. 

## SLAC

> SLAC (Single-Likelihood Ancestor Counting) uses a combination of maximum-likelihood (ML) and counting approaches to infer nonsynonymous (dN) and synonymous (dS) substitution rates on a per-site basis for a given coding alignment and corresponding phylogeny. Like FEL, this method assumes that the selection pressure for each site is constant along the entire phylogeny. ...SLAC may not be accurate for data sets with high divergence levels.

## RELAX

> RELAX is a hypothesis testing framework that asks whether the strength of natural selection has been relaxed or intensified along a specified set of test branches. RELAX is therefore not a suitable method for explicitly testing for positive selection. Instead, RELAX is most useful for identifying trends and/or shifts in the stringency of natural selection on a given gene. RELAX requires a specified set of "test" branches to compare with a second set of "reference" branches (note that all branches do not have to be assigned, but one branch is required the test and reference set each). RELAX begins by fitting a codon model with three ω classes to the entire phylogeny (null model). RELAX then tests for relaxed/intensified selection by introducing the parameter k (where k≥0), serving as the selection intensity parameter, as an exponent for the inferred ω values: ω<sup>k</sup>...RELAX then conducts a Likelihood Ratio Test to compare the alternative and null models. 

Output:
 * `<input_file>.RELAX.json` - if run completes successfully.
 * `messages.log` - log file full of log file things. Never found a use for it.
 * `errors.log` - if the run terminates unsuccessfully. 
