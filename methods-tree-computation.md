# Tree Computation
## Maximum Likelihood & Bayesian Paradigms for Tree Computation
Note that these are not two opposing frameworks, nor are they the *only* frameworks for the interpretation of probability.  The (opposing) counterpart to Bayesian statistics is frequentist statistics, which is out of the scope of this tutorial, but quite nicely summed up as follows:

![xkcd1132](https://imgs.xkcd.com/comics/frequentists_vs_bayesians.png)

The bottom line is:
- **Maximum likelihood** methods compute the most likely tree that evolved the observed sequence data. Answers the question: "*Out of all these models, which is the most likely one to have arisen out of the given data?*" Note that ML can only compare between models to pick the most appropriate one. It is unable to assess the correctness of a model, i.e. it could be picking the least terrible out of a bunch of terrible models.
- **Bayesian** methods have an extra step of modeling the uncertainty we have about any previous relevant information as a probability distribution by itself. This is called the *prior*. 
- ML trees can deal with sequence data that doesn't have dates (branch lengths indicate sequence similarity). Bayesian trees can compute time-stamped trees (branch lengths indicate passage of time)

*Note: all this is actually much easier in maths, because many things get lost in translation when attempting to convert these concepts into English. Ultimately, it's all just calculus.*

## ML Trees

### Consensus Tree vs. Best (Maximum Likelihood) Tree
They both contain relevant information. 

The **best tree** is the tree that best fits the input data, the equivalent of a point estimate. Mathematically, it's literally the *maximum* likelihood tree. In a sense, it's *overfitted*.

The **consensus tree** gives information on which sub-structures in a tree are well-supported - that is, which groups consistently appear. In the frequentist sense, these values tell you how probable that structure is. This directly translates to the generalizability of the data.

In practice, you can present a happy middle ground by projecting support values onto the best tree, or just present the consensus tree. 

### Statistical Support

ML trees use *bootstrap values* (an explanation of what that is will be forthcoming in future). 

To figure out how many bootstrap iterations to use, that's actually a function of the number of sequences in your dataset. As the number of sequences increase, the number of possible trees increase extremely dramatically as well (I forget the actual Big O function, but there's a factorial in there somewhere). As such, for very large datasets, no ML-based searching algorithm can search a feasible size of all possible trees within a feasible period of time. In general, if the data has very long alignments, the chance of getting an optimal tree increases. If the data has shorter alignments, finding the global maxima will be harder. 

## Bayesian Trees

### Statistical Support

BEAST trees use *highest posterior density* (HPD) intervals. The HPD interval is the equivalent of the better-known *confidence interval* in frequentist statistics, in that it is the *shortest interval on the domain which has a 95% probability mass*. This means that (a) it's possible for HPD intervals to be negative, even if your data consists only of positive values, and (b) it's possible, but highly improbable, for your estimate to lie *outside* the HPD interval. Note that HPD intervals (and any statistical analyses, for that matter) can be problematic if the posterior turns out to be bimodal. But sometimes, to quote Alexei Drummond, a bimodal posterior really is the best answer that you can get. 

## An Overview of Tree Computing Software

`FastTree`, `IQ-tree`, `RAxML` and `PhyML` all compute ML trees; BEAST is the only program we use that computes Bayesian trees. 


### FastTree
 - Fast, as you may have picked up from the name. Typically terminates within minutes, even with thousands of sequences.
 - Computes only one tree, so the results of FastTree are questionable not so much because of the accuracy of the tree, but because it doesn't give a way to assess the quality of the result (e.g. by likelihood or empirical support).
 - Anecdotally, seems reasonably accurate at computing the initial bifurcations, i.e. identifying major clades. Might get confused by sequences that could go either way. For instance, in the following example, it's clear the sequences 1 and 3 belong to different clades, but FastTree might get confused by where sequence 2 should go:
 
```
sequence1: AAAAAA
sequence2: AAAGGG
sequence3: GGGGGG
```

### IQTree
 - ML-based. 
 - Not terribly fast. It *could* be faster than RAxML; I've never really tested it in large runs.
 - From some small test runs, IQ-Tree and FastTree seem to produce the same results, but IQ-Tree is usually slower. 

### RAxML
 - Very slow, so only used in production when we have to compute publication-quality trees, with a certain number of iterations (>500 or >1000 required for publication, depending on who you ask) - as such, would typically take a week. 
 - Has PTHREADS for multiple-CPU parrallelization, and an SSE-extension to speed things up just that much faster - but still slow.
 - Too slow - only use on the HPC!
 - Will only terminate within a reasonable amount of time for <1000 sequences (and that's still pushing it). 
 
### BEAST
 - Bayesian paradigm, so you'll get something like P(Tree|Models, ModelParams). 
 - With a nice point-and-click interface, so probably the most user-friendly. Also has helper programs `BEAUTi` and `Tracer`.
 - Also very slow, but anecdotally faster than RAxML. Send your jobs to M3 for production runs.
 - Has GPU support, which on benchmark tests, gives a ~4x speedup on M3's K80 GPUs based on benchmark tests.

