# Introduction to Multiple Sequence Alignment

*Alignment* is a mechanical procedure to a set of DNA sequences look pretty, i.e. all the letters line up. For instance, given this small bunch of 3 short sequences:

```
GCCAGCCTTAG
AAAGCCTTT
CAAGGGCTAG
```

We want to line up the letters, inserting gaps '-' as necessary, to get this:
```
GCCA--GCCTTAG
---AAAGCCTTT-
--CAAGGGCTAG-
```

This procedure is called *multiple sequence alignment*.  It's not purely cosmetic - many programs will only accept aligned DNA sequences.  It's also much easier on the eyes to look at an aligned dataset in order to, for instance, identify a SNP.  There's no purely algorithmic procecdure for arriving at a nice, clean aligned dataset, otherwise I'd have written a script for it a long time ago.  A sequence alignment program like `MAFFT` can get you 90% of the way, but there are always several special cases which require expert (and subjective) judgement.

## Preparing your data for MSA

Conventional wisdom dictates that manual curation of alignments is absolutely necessary, precisely because of the possibility of special cases as mentioned above. However, with increasing volumes of data, it's becoming impossible to even open the dataset in a text editor, much less edit anything. Traditionally, we've been able to manually screen special cases individually (e.g. some sequence has an uncomfortably long sequence of `n`'s, indicating a technical sequencing error of some kind), and decide whether or not to discard them individually.  With large amounts of data, it may be more viable to prescribe a set of minimum quality requirements (e.g. "the total number of `n`s in a sequence cannot be more than 5% of the total sequence length) and apply them across the whole dataset. Of course, there's always the possibility that unknown special cases will slip by, but we can assume (and statistically argue) that such cases will be too few to threaten the integrity of the study.  After all, Google can't clean its data. 

A standard checking set that I normally use is:
* The *total ungapped length* of each sequence should be at least 70% of the median ungapped sequence length (ungapped sequence length = sequence length after all gaps `"-"` and `"n"` have been removed)
* The length of the largest gap in each sequence should not be more than 25% of the median ungapped sequence length. 

Fortunately, many of the tree-building methods (which the aligned sequences are fed into as input) are *fault tolerant*, i.e. they are quite resistant to the inteference of a few outliers while still managing to present the overall trend.  For instance, maximum likelihood statistics or bootstrap support will mitigate the effects of a few outlier sequences (both methods involve recomputing a tree over and over again, using the same dataset, and selecting the most commonly occuring tree as the best one). 

For trees that are initially computed for the purposes of exploring the dataset, there's no maximum likelihood computation or bootstrap support, so how can we be confident that our single tree is sufficiently representative of the dataset?

(*Too jargony. Simplify*)

Other biological considerations:

* Single- or double- nucleotide gaps are far less probable than triple-nucleotide gaps, because inserting 1 or 2 gaps will result in dramatically different amino acid chains, which the organism would probably not have been able to survive. Ideally, we should have no gaps at all. 

* Other biological considerations: e.g. A gene should start with a start codon and stop with a stop codon. You can't have a start or stop codon in the middle of a gene. 

Next tutorial - we'll look into using `MAFFT` for multiple sequence alignment.
