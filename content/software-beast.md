# BEAST Tutorial

There are two versions of BEAST: BEAST1, and BEAST2. Their interfaces are very similar, and I'm slowly migrating toward BEAST2, because it can do everything that BEAST1 can do, and more. 

### The Best Quickstart Tutorial I Know Of

This is a cheat - I'm not actually writing the tutorial, but dropping a link to an [already excellent tutorial](https://github.com/trvrb/dynamics-practical) written by Trevor Bedford.  That tutorial gives a demo of a whole analysis pipeline from `BEAUTI` through to `Tracer`, `Figtree` and `TreeAnnotator`. 

This set of [Taming-the-Beast(2)](https://taming-the-beast.github.io/) tutorials are also useful, though applicable only to BEAST 2. 

### Useful Links

 - The [BEAST2 tutorials](https://www.beast2.org/tutorials/)
 - The [exercises and tutorials](https://taming-the-beast.github.io/) from the Taming the Beast 2017 workshop are also good.
 - A temporary [tutorial on tip-dating](https://github.com/Taming-the-BEAST/Basic-tip-dating) in BEAST2, written by Louis du Plessis.

Ultimately, though, the most difficult question is about the most appropriate choice of parameters to select for the given study. 

### Miscellaneous Tips and Tricks

 - Neither BEAST1 nor BEAST2 can handle very large data sets - 300 - 400 is a good number; 600 is pushing it. Fancy BEAST2 add-on packages tend to run even slower. 
 - 200 million is a good chain length. In a sense, it's not worth running for any longer because the data set may be too highly correlated anyway, which means that there's a problem with the data. 
 - Do BEAST runs in triplicate, i.e. repeat the same run three times to get at least one good run. 
 - When in doubt, use a uniform prior over a very large interval, like 0 to 10,000. The reason for this is that the uniform distribution really does honestly reflect your state of mind - you really have no idea what the best parameter choice is - and so is the most intellectually honest answer. 
