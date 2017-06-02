# Alignment
(WIP)


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

This procedure is called *multiple sequence alignment*, or just *alignment* for short.  It's not purely cosmetic - many programs will only accept aligned DNA sequences. Roughly speaking, we gauge the goodness of an alignment with the following considerations:

* Single- or double- nucleotide gaps are far less probably than triple-nucleotide gaps, because inserting 1 or 2 gaps will result in dramatically different amino acid chains, which the organism would probably not have been able to survive. Ideally, we should have no gaps at all. 

* Other biological considerations: e.g. A gene should start with a start codon and stop with a stop codon. You can't have a start or stop codon in the middle of a gene. 

## `MAFFT`
The program of choice to use is [MAFFT](http://mafft.cbrc.jp/alignment/software/), which is probably an abbreviation of some kind. It will do most of the work, and quite quickly as well. 

