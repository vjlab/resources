# Tree Computation Part 1 - Theory

**Warning: Mathematically intensive**. I haven't figured out how to explain most of this in English yet. All this is actually much easier in maths, because many things get lost in translation when attempting to convert these concepts into English. Ultimately, it's all just calculus.

## Maximum Likelihood & Bayesian Paradigms for Tree Computation
Note that these are not two opposing frameworks, nor are they the *only* frameworks for the interpretation of probability.  The (opposing) counterpart to Bayesian statistics is frequentist statistics, which is out of the scope of this tutorial.

The key points are:
- **Maximum likelihood** methods compute the most likely tree that evolved the observed sequence data. Answers the question: "*Out of all these models, which is the most likely one to have arisen out of the given data?*" Note that ML can only compare between models to pick the most appropriate one. It is unable to assess the correctness of a model, i.e. it could be picking the least terrible out of a bunch of terrible models.
- **Bayesian** methods have an extra step of modeling the uncertainty we have about any previous relevant information as a probability distribution by itself. This is called the *prior*. 
- ML trees can deal with sequence data that doesn't have dates (branch lengths indicate sequence similarity). Bayesian trees can compute time-stamped trees (branch lengths indicate passage of time)

## ML Trees

### Consensus Tree vs. Best (Maximum Likelihood) Tree
They both contain relevant information. 

The **best tree** (named as such because RAxML will prefix the phrase `besttree` to the output) is the tree that best fits the input data, the equivalent of a point estimate. Mathematically, it's literally the *maximum* likelihood tree. 

The **consensus tree** gives information on which sub-structures in a tree are well-supported - that is, which groups consistently appear. This directly translates to the generalizability of the data.

So which is the "true" tree? This presents a bit of a philosophical pickle because, by definition of the word "maximum", there can be only *one* maximum likelihood tree (other than the extremely unlikely event of a multi-modal likelihood landscape), so it's difficult to assess the correctness of this tree.  The consensus tree, which is an aggregation of all sampled trees, is almost surely not the same as the maximum likelihood tree, because, as mentioned, all save one of the sampled trees will be suboptimal. In practice, you can use a happy middle ground by projecting support values onto the maximum likelihood tree. 

### Variants of consensus trees

[Source](https://www.stat.wisc.edu/~larget/Genetics629/lec6-4.pdf)

 - A **strict consensus tree** shows only the substructures (or "clades") which appear in every sampled tree. 
 - A **majority rule consensus tree** shows only the substructures which appear in at least 50% of the sampled trees.
 - A **priority consensus tree** adds substructures to the majority rule consensus tree in order of decreasing frequency in the sample provided that these new substructures do not conflict with a substructure with higher frequency.
 
Personal note: I've never used any of these before, because it's simpler (i.e. more interpretable) to use a consensus tree with, say, substructures that have <70 bootstrap support collapsed. In RAxML, this is the option `-J T_70`.

### Statistical Support - Bootstrap

The following explanation is adapted from Wikipedia, and [Efron 1979](https://projecteuclid.org/euclid.aos/1176344552). Say we get a sample of size *n* of people from a population, and we calculate the sample mean height. How reliable is this sample mean, in the sense that if we had gotten a different sample of *n* people, how similar would the sample mean height of this second sample be to our current sample height? And how would it all compare to the true population average height?

The *bootstrap* procedure is as follows:

1. Select *n* samples *with replacement* from our current sample of size *n*, where each sample has a probability of *1/n* to be chosen. Compute the mean of this new sample. 
2. Repeat step 1 an arbitrarily large number of times, say, 1000 times. 
 
You would then get 1000 different (bootstrapped) values of the average height, which you can compute variance on. If the bootstrap has large variance (i.e. a large CI), then you can say that your dataset point estimates are not very representative of the true population parameters. 

ML trees use *bootstrap values* in a similar manner to compute statistical support for each branch, except that this time, the *site* is value of interest, rather than height (or, well, the *transition probabilities* between sites, which is directly computed from the nucleotide values themselves). From [Felsenstein 1985](http://biostat.jhsph.edu/~jleek/teaching/2011/754/reading/felsenstein.pdf), given a dataset of *n* sequences of length *m* sites (nucleotide or amino acid):

1. Select *m* sites *with replacement*, where each site has a probability of *1/m* to be chosen. 
2. Compute the nucleotide substitution matrix from this new sample. Not sure if you compute a tree at this step. 
3. Repeat steps 1 and 2 an arbitrarily large number of times. 

Felsenstein notes that this procedure effectively treats evolution at each site as independent between sites, which is almost certainly wrong. Treating positively(negatively) correlated sites as independent would result in confidence intervals which are larger(smaller) than they should be. But there's no way in advance to compute correlation between sites. 

(Felsenstein chose to generate bootstrap replicates by randomly choosing *sites* with replacement because the dataset itself, with *n* sequences, all of length *m* nucleotide, would be a random sample from the set of *all possible nucleotide sequences* of length *m*. However, I see no reason why generating bootstrap replicates by randomly selecting *sequences* with replacement would be different - after all, in the earlier height experiment, we randomly select *people*, where *height* is the property that we're interested in. Similarly, we would randomly select *sequences*, where *nucleotide sequence* is the property that we're interested in.)

## How many Bootstraps?

To figure out how many bootstrap iterations to use, that's actually a function of the number of sequences in your dataset. As the number of sequences increase, the number of possible trees increase extremely dramatically as well (I forget the actual Big O function, but there's a factorial in there somewhere). As such, for very large datasets, no ML-based searching algorithm can search a feasible size of all possible trees within a feasible period of time. In general, if the data has very long alignments, the chance of getting an optimal tree increases. If the data has shorter alignments, finding the global maxima will be harder. 

A [best practice](https://groups.google.com/forum/#!topic/iqtree/0mwGhDokNns) recommendation is as follows:


>During the tree search, IQ-TREE samples a lot of locally optimal trees and produce a locally optimal tree in each iteration. The log-likelihood of the locally optimal trees are printed after every 10 iterations. If you want to see the log-likelihood of all locally optimal trees, turn on the flag -v (verbose). Toward the end of the search, if the log-likelihoods seem to converge (some iterations produce the same log-likelihood) then you might only need to repeat the search few more times. If they do not, you should repeat the search as many times as possible. 

>...large log-likelihood variance among IQ-TREE runs often means that your data does not contain enough phylogenetic signal. In such case, you have do some statistical tests to access the branch support (UFBoot, aLRT, standard bootstrap). With little data, even if the optimal tree could be found, it might still look very different from the true tree. 


My contentions with this best practice are:

 - Multiple runs, say, 5 separate runs, to get different local optima, each with 1000 steps, may not produce a superior tree to a single run with 5000 steps - because the separate runs could be overlapping and searching the same space by coincidence. The probability of this happening decreases as tree space increases. It's more predictable to use a single run with 5000 steps, with an appropriately chosen step-size or perturbation to escape local optima (see the link for how to do this). This is a bit of an open problem, with the following analogy:
 
> Say you've lost a coin in a very large house, with 3 levels. Which strategy is better: (A) get 3 people to search for the coin, for 1 hour concurrently, where each persons starts on a different level. Each person remembers where he last searched so that he won't go over the same ground again, but different people may accidentally search the same ground. (B) get 1 person to search for 3 hours.
 
 - There may be no such thing as a true tree. In the language of machine learning, computing a tree is an unsupervised problem. 

## Bayesian Trees

### Statistical Support

BEAST trees use *highest posterior density* (HPD) intervals. The HPD interval is the equivalent of the better-known *confidence interval* in frequentist statistics, in that it is the *shortest interval on the domain which has a 95% probability mass*. This means that (a) it's possible for HPD intervals to be negative, even if your data consists only of positive values, and (b) it's possible, but highly improbable, for your estimate to lie *outside* the HPD interval. Note that HPD intervals (and any statistical analyses, for that matter) can be problematic if the posterior turns out to be bimodal. But sometimes, to quote Alexei Drummond, a bimodal posterior really is the best answer that you can get. 
