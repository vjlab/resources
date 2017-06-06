# Introduction to Multiple Sequence Alignment

*Alignment* is a mechanical procedure to line up all the letters in a set of DNA sequences. For instance, given this small bunch of 3 short sequences:

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

This procedure is called *multiple sequence alignment*.  It's not purely cosmetic - many programs will only accept aligned DNA sequences.  It's also much easier on the eyes to look at an aligned dataset in order to, for instance, identify a SNP.  There's no purely algorithmic procecdure for arriving at a nice, clean aligned dataset, otherwise I'd have written a script for it a long time ago.  A sequence alignment program like `MAFFT` or `Clustal` can get you 90% of the way, but there are always several special cases which require expert (and subjective) judgement.

In this series of tutorials about alignment, we'll go through the most involved MSA process in a usual project, which is the initial alignment after recieving raw data.

## MSA for data cleaning
The general procedure is (not a hard and fast procedure!):

0. Preliminary duplicate removal - this applies to all manner of data preparation, not just for alignment. I form a new `name_id` column by concatenating the `isolate name` and `isolate ID`. Duplicate `name_id`s are then removed by selecting the longest HA sequence (randomly pick one if there's a tie). After this, we might still have isolate names with multiple isolate IDs, i.e. where multiple labs sequenced the same sample. Hopefully, these are few enough to evaluate individually on a case-by-case basis, picking whichever has the most complete metadata (e.g. full dates, locations, etc.). 
1. Do a quick-and-dirty alignment. Generally, this means that we only need, say, 90% of the letters to line up; there can be some single- or double-nucleotide confusion somewhere. In any case, there will still be "bad" sequences in there, throwing everything off (e.g. sequences with large chunks of `"n"`s, sequences which look so different from the others that they must've been some kind of sampling error because organisms just don't mutate that fast, etc.). In fact, this initial alignment is exactly to identify these bad sequences. 
2. Trim the non-coding regions outside the reading frame.  We're not usually interested in these anyway.
3. Discard any bad sequences that you can find. 
4. Do another round of alignment, with a more accurate algorithm. 
5. A final round of manual cleaning, with any kind of gap deletion or nucleotide rearrangements required. 

## Preparing your data for MSA

Conventional wisdom dictates that manual curation of alignments is absolutely necessary. However, with increasing volumes of data, it's becoming impossible to even open the dataset in a text editor, much less edit anything. Traditionally, we've been able to manually screen special cases and decide whether or not to discard them individually.  With large amounts of data, it may be more viable to prescribe a set of minimum quality requirements (e.g. "the total number of `n`s in a sequence cannot be more than 5% of the total sequence length) and apply them across the whole dataset. Of course, there's always the possibility that unknown special cases will slip by, but we can assume (and statistically argue) that such cases will be too few to threaten the integrity of the study.  After all, Google can't clean its data. 

A standard QC set that I normally use to form exploratory trees is:
* The *total ungapped length* of each sequence should be at least 70% of the median ungapped sequence length (ungapped sequence length = sequence length after all gaps `"-"` and `"n"` have been removed)
* The length of the largest gap in each sequence should not be more than 25% of the median ungapped sequence length. 

Forming publication-quality trees will require much more stringent quality checks. 

Fortunately, many of the tree-building methods (which the aligned sequences are fed into as input) are *fault tolerant*, i.e. they are quite resistant to the inteference of a few outliers while still managing to present the overall trend.  For instance, maximum likelihood statistics or bootstrap support will mitigate the effects of a few outlier sequences (both methods involve recomputing a tree over and over again, using the same dataset, and selecting the most commonly occuring tree as the best one). 

For trees that are initially computed for the purposes of exploring the dataset, there's no maximum likelihood computation or bootstrap support, so how can we be confident that our single tree is sufficiently representative of the dataset?

(*Too jargony. Simplify*)

Other biological considerations:

* Single- or double- nucleotide gaps are far less probable than triple-nucleotide gaps, because inserting 1 or 2 gaps will result in dramatically different amino acid chains, which the organism would probably not have been able to survive. Ideally, we should have no gaps at all. 

* Other biological considerations: e.g. A gene should start with a start codon and stop with a stop codon. You can't have a start or stop codon in the middle of a gene. 

Next tutorial - we'll look into using `MAFFT` for multiple sequence alignment.

## Note: Some Tree Considerations
`FastTree` and `IQ-Tree` do not seem to consider gaps `"-"` as differences. That is, the number of similar letters between `acgtacgt` and `acgt----` is 4, but the number of different letters is 0. Therefore, as the variability that you expect to see in your dataset increases, you should likewise be increasingly punitive on removing sequences with large gaps. 
* If your dataset consists of very similar sequences, then a sequence with a gap is likely the same as every other sequence, and will correctly cluster in the appropriate clade.
* If your dataset consists of very dissimilar sequences, then the tree-drawing software may have multiple matches to cluster that gappy sequence with, and it may be computationally impossible to break these ties.  In software which does multiple tree computations to give statistical support of some kind (e.g. BEAST), this will result in fairly different trees in each run, when removing that gappy sequence altogether would give a much better concensus tree. In ML software, including that gappy sequence would make likelihood computations extremely path-dependant, making it difficult to arrive at the same ML tree over different runs.

Given the following fasta file:
```
>r1
ACGTACGTACGT
>r2
ACGTTGCAACGT
>r3
ACGT----ACGT
>r4
ACGTACGT----
>r5
ACGTTGCA----
```
`Fasttree` produced a tree like:

r3<br>
|<br>
|<br>
r1<br>
|<br>
|<br>
r4<br>
|<br>
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| r2<br>
----------|<br>
&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| r5<br>
                 
And `IQ-tree` produced a tree like:

r1<br>
|<br>
|&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| r2<br>
-----------|<br>
|&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| r5<br>
|<br>
|<br>
| r3<br>
|<br>
| r4
