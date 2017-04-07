# RAxML (WIP)
*Don Teng, April 2017*

This tutorial is meant to be a condensed version of the [RAxML v8.2 manual](http://sco.h-its.org/exelixis/resource/download/NewManual.pdf), as a sort of quickstart user guide. 

The executable currently in M3 is `raxmlHPC-AVX`, so at the bottom of your SLURM script, we use the commands:

```
module load raxml/8.2.9
raxmlHPC-AVX2 ...
```

### Commonly Specified Options
`-m <model>` - Specifies the substitution model to be used. The most commonly used model appears to be `GTR GAMMA`
`-p <random seed>` - Sets the random seed for reproducibility.
`-s <input_alignment_file>` - Specify the input alignment file. RAxML accepts relaxed `phy`, `phy`, or `fasta`.
