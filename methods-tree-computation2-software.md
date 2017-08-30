# Tree Computation Part 2 - Software

`FastTree`, `IQ-tree`, `RAxML` and `PhyML` all compute ML trees; `BEAST` is the only program we use that computes Bayesian trees.

### FastTree

 - Fast, as you may have picked up from the name. Typically terminates within minutes, even with thousands of sequences.
 - Computes only one tree, so the results of FastTree are questionable not so much because of the accuracy of the tree, but because it doesn't give a way to assess the quality of the result (e.g. by likelihood or empirical support).
 - Anecdotally, seems reasonably accurate at computing the initial bifurcations, i.e. identifying major clades. Might get confused by sequences that could go either way. For instance, in the following example, it's clear the sequences 1 and 3 belong to different clades, but FastTree might get confused by where sequence 2 should go:
 - Again, anecdotally, FastTree still seems to produce similar results to ML tree programs if the sequences are long enough (>1000 nucleotides), because longer sequences have more "phylogenetic signal" (it's easier for converge to a transition matrix for the chosen nucleotide substitution model, because there are more sites). 

```
sequence1: AAAAAA
sequence2: AAAGGG
sequence3: GGGGGG
```

### IQTree

 - ML-based.
 - Not terribly fast. It could be faster than RAxML; I've never really tested it in large runs.
 - From some small test runs, IQ-Tree and FastTree seem to produce the same results, but IQ-Tree is usually slower.

### RAxML

 - Very slow, so only used in production when we have to compute publication-quality trees, with a certain number of bootstrap iterations. Only use on the HPC!
 - Has PTHREADS for multiple-CPU parrallelization, and an SSE-extension to speed things up just that much faster - but still slow.
 - Will only terminate within a reasonable amount of time for <1000 sequences (and that's still pushing it).

BEAST

 - Bayesian paradigm, so you'll get something like P(Tree|Models, ModelParams).
 - With a nice point-and-click interface, so probably the most user-friendly. Also has helper programs BEAUTi and Tracer.
 - Also very slow, but anecdotally faster than RAxML. Send your jobs to M3 for production runs.
 - Has GPU support, which on benchmark tests, gives a ~4x speedup on M3's K80 GPUs based on benchmark tests.
