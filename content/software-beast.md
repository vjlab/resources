# BEAST Tutorial

There are two versions of BEAST: BEAST1, and BEAST2. To compare the two:

 - BEAST1 can automatically parse the calendar dates at the end of sequence names into decimal dates, and allows some dates to have variable precision, others exact precision. With BEAST2, you'll have the extra hassle of preparing a text file of decimal dates, and setting dates with variable precision is much more cumbersome. 
 - BEAST2, however, has lots of fancy add-on packages which contain features not available at all in BEAST1. 

### Useful Links

 - An [excellent BEAST 1 tutorial](https://github.com/trvrb/dynamics-practical) written by Trevor Bedford.  That tutorial gives a demo of a whole analysis pipeline from `BEAUTI` through to `Tracer`, `Figtree` and `TreeAnnotator`. 
 - This set of [Taming-the-Beast(2)](https://taming-the-beast.github.io/) tutorials are also useful, though applicable only to BEAST2. 
 - Sebastian Duchene's [phylo workshop](https://github.com/sebastianduchene/phyloworkshop_2017) is an excellent starting point for BEAST2. 
 - A temporary [tutorial on tip-dating](https://github.com/Taming-the-BEAST/Basic-tip-dating) in BEAST2, written by Louis du Plessis.

### Miscellaneous Tips and Tricks

 - Neither BEAST1 nor BEAST2 can handle very large data sets - 300 - 400 is a good number; 600 is pushing it. Fancy BEAST2 add-on packages tend to run even slower. 
 - 200 million is a good chain length. It's not worth running for any longer because the data set may be too highly correlated anyway, which means that there's a problem with the data. 
 - Do BEAST runs in triplicate, i.e. repeat the same run three times to get at least one good run. 
 - When in doubt, use a uniform prior over a very large interval, like 0 to 10,000. The reason for this is that the uniform distribution really does honestly reflect your state of mind - you really have no idea what the best parameter choice is - and so is the most intellectually honest answer. 
