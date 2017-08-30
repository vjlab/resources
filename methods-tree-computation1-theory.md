# Tree Computation Part 1 - Theory
## Maximum Likelihood & Bayesian Paradigms for Tree Computation
Note that these are not two opposing frameworks, nor are they the *only* frameworks for the interpretation of probability.  The (opposing) counterpart to Bayesian statistics is frequentist statistics, which is out of the scope of this tutorial.

The key points are:
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

### Variants of consensus trees

[Source](https://www.stat.wisc.edu/~larget/Genetics629/lec6-4.pdf)

 - A **strict consensus tree** shows only the substructures (or "clades") which appear in every sampled tree. 
 - A **majority rule consensus tree** shows only the substructures which appear in at least 50% of the sampled trees.
 - A **priority consensus tree** adds substructures to the majority rule consensus tree in order of decreasing frequency in the sample provided that these new substructures do not conflict with a substructure with higher frequency.
 
Personal note: I've never used any of these before, because it's simpler (i.e. more interpretable) to use a consensus tree with, say, substructures that have <70 bootstrap support collapsed. In RAxML, this is the option `-J T_70`.

### Statistical Support

ML trees use *bootstrap values* (an explanation of what that is will be forthcoming in future). 

To figure out how many bootstrap iterations to use, that's actually a function of the number of sequences in your dataset. As the number of sequences increase, the number of possible trees increase extremely dramatically as well (I forget the actual Big O function, but there's a factorial in there somewhere). As such, for very large datasets, no ML-based searching algorithm can search a feasible size of all possible trees within a feasible period of time. In general, if the data has very long alignments, the chance of getting an optimal tree increases. If the data has shorter alignments, finding the global maxima will be harder. 

## Bayesian Trees

### Statistical Support

BEAST trees use *highest posterior density* (HPD) intervals. The HPD interval is the equivalent of the better-known *confidence interval* in frequentist statistics, in that it is the *shortest interval on the domain which has a 95% probability mass*. This means that (a) it's possible for HPD intervals to be negative, even if your data consists only of positive values, and (b) it's possible, but highly improbable, for your estimate to lie *outside* the HPD interval. Note that HPD intervals (and any statistical analyses, for that matter) can be problematic if the posterior turns out to be bimodal. But sometimes, to quote Alexei Drummond, a bimodal posterior really is the best answer that you can get. 
