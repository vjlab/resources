# `MAFFT`
The program of choice to use is [MAFFT](http://mafft.cbrc.jp/alignment/software/). It will do most of the work, and quite quickly as well. MAFFT also has [excellent documentation](http://mafft.cbrc.jp/alignment/software/manual/manual.html). 

### Normal MAFFT
To do a basic run of MAFFT, use, on the command line:

```
mafft input_file.fasta > output_file.fasta
```

This will work well almost any time - it's just a matter of optimizing the speed and the needs of your study. 

### Speed-oriented
If you have, roughly, >4000 sequences, the normal version of MAFFT may run for too long - up to an hour, which is not too bad, but not necessary if we only need a rough alignment. This works especially well as a "first pass" alignment if you don't know if your sequences will be of approximately the same length, or, if so, the relative distributions of sequence lengths. 
```
mafft --retree 1 --maxiterate 0 input.fasta > output.fasta
```

In the manual, this command is officially recommended for >2000 sequences.  From my own tests, it runs 2-3x faster than the normal command, and should only be used for >4000 sequences (any dataset with fewer than 4000 would have unacceptable losses in accuracy for minimal speed improvements). If this speed-oriented variant is used, there should be a manual cleaning step to follow up that first "makes things easier for MAFFT" (e.g. trimming the non-coding regions, reducing the number of sequences by removing sequences with large gaps, etc.), followed by a normal run of mafft.

### Accuracy oriented - sequences of different lengths
If your sequences can be markedly different in length (e.g. if you expect some of your sequences to comprise of just 1 gene, and yet other sequences to be full genomes), use a local alignment option:

```
mafft --localpair --maxiterate 1000 input.fasta > output.fasta
```

The [local alignment algorithm](https://en.wikipedia.org/wiki/Needleman%E2%80%93Wunsch_algorithm) finds the best position of a short string within a longer string, e.g. finding `"wunder"` in `"it's a wonderful day"`, minimizing the number of gaps inserted and number of mismatched letters. Officially recommended for <200 sequences, but my tests showed that these were still manageable on the HPC for up to 4000 full dengue 1 - 4 sequences (terminated in less than half an hour).

### Accuracy oriented - sequences of approximately similar lengths
If your sequences are of approximately the same length, use a global alignment option:

```
mafft --globalpair --maxiterate 1000 input.fasta > output.fasta
```

A [global alignment algorithm](https://en.wikipedia.org/wiki/Smith%E2%80%93Waterman_algorithm) lines up two sequences of approximately the same length; MAFFT would then do global alignment for all possible pairs within the dataset. I'm not exactly sure whether this is superior in accuracy to the "normal" run, but it's certainly slower. 

~ End ~

(Note: I personally dislike the prefixes "global" and "local" because these seem to imply that they are two ends of a spectrum of some kind, when they actually just refer to two different scenarios: "local alignment" finds a short string within a long string, "global alignment" lines up two strings of about the same length. See [this](https://biology.stackexchange.com/questions/11263/what-is-the-difference-between-local-and-global-sequence-alignments) stackexchange post for details.)
