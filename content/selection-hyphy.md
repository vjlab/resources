# Selection Analysis with `HyPhy`

This tutorial covers using my Python3 `wrapomatic` wrapper library for two commonly-used methods: SLAC and RELAX. 

`wrapomatic` was built and tested on a MacOS X (High Sierra), HYPHY 2.3.720180108beta(MP). If you already have it installed, use `$ HYPHYMP -v` to check which version you've got. New 2.3.x versions seem to come out at least once a month with single bug fixes, so this wrapper *should* (fingers-crossed) work with any 2.3.x version. 

## Installation

Follow the [installation instructions](https://veg.github.io/hyphy-site/installation/) on their website. Somewhat long, but should be straightforward. 

## SLAC (WIP)

> SLAC (Single-Likelihood Ancestor Counting) uses a combination of maximum-likelihood (ML) and counting approaches to infer nonsynonymous (dN) and synonymous (dS) substitution rates on a per-site basis for a given coding alignment and corresponding phylogeny. Like FEL, this method assumes that the selection pressure for each site is constant along the entire phylogeny. ...SLAC may not be accurate for data sets with high divergence levels.

## RELAX

> RELAX is a hypothesis testing framework that asks whether the strength of natural selection has been relaxed or intensified along a specified set of test branches. RELAX is therefore not a suitable method for explicitly testing for positive selection. Instead, RELAX is most useful for identifying trends and/or shifts in the stringency of natural selection on a given gene. RELAX requires a specified set of "test" branches to compare with a second set of "reference" branches (not all branches have to be assigned, but one branch is required the test and reference set each). RELAX begins by fitting a codon model with three ω classes to the entire phylogeny (null model). RELAX then tests for relaxed/intensified selection by introducing the parameter k (where k≥0), serving as the selection intensity parameter, as an exponent for the inferred ω values: ω<sup>k</sup>...RELAX then conducts a Likelihood Ratio Test to compare the alternative and null models. 

> cite: Wertheim, JO et al. "RELAX: detecting relaxed selection in a phylogenetic framework." Mol. Biol. Evol. 32, 820–832 (2015).

RELAX compares a set of labelled branches (labelled `{test}`) against the rest of the unlabelled branches to see if the labeled and unlabelled branches experience significantly different selection pressures.  This means *all* branches, both internal and terminal branches (typically, a whole clade). Hypothesis setup: ω = dNdS of the reference branches, ω<sup>k</sup> = dNdS of the test branches. 

 * M0: k = 1
 * M1: k != 1
 
Output files:

 * `<input_file>.RELAX.json` - if run completes successfully.
 * `messages.log` - log file full of log file things. Never found a use for it.
 * `errors.log` - if the run terminates unsuccessfully. 

### 1. Label Your Tree Branches

 * Go to this [phylotree.JS](http://phylotree.hyphy.org/) widget to mark your branches. You can click on all the branches that you want labelled. 
 * Pro-tip: to make life easier, click on the important ancestral nodes of the branches that you want select, and select "All descendant branches" to select a whole bunch at a shot. You may still have to manually select a few stragglers; the widget doesn't work perfectly for multifurcating trees (but still does 90% of the job). 
 * To save the labelled tree, click "Newick>Export". The labelled branches will be marked with `{foreground}`. Save the tree string in a new text file. 
 * Open your new labelled tree in TextWrangler or something, and replace `{Foreground}` with `{test}` (You're supposed to be able to do this within the JS widget, but I could never get it to work). 

### 2. Prepare A Single Input File

This is just a fasta file of your sequences, and the labelled tree string in Newick format at the bottom. 

### 3. Use `Wrapomatic`

Within the Python3 environment of your choice:

```
import wrapomatic as wrp
# Init HyphyRelax object
hx = wrp.HyphyRelax()
# Fill in input file name from step 2
hx.data_file="path/to/file.fas"
hx.run()
```
Expected output:
```
Running HYPHYMP:RELAX
Genetic code = universal code
Input file = input_file.fas
Branches used as _test_ set: Branches labelled 'test'
RELAX analysis type: Run only the RELAX test (2 models)
STDOUT output file: input_file.fas_results.out
Done in 289.18s
```
It's that simple. 
