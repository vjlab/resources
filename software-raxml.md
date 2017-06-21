# RAxML (WIP)
*Don Teng, 6 June 2017*

## Introduction
`RAxML` takes a `.fasta` or `.txt` file of aligned sequences as input, and computes maximum likelihood trees. 

## Installation
Go straight [here](http://www.sfu.ca/biology2/staff/dc/raxml/), and follow their steps accordingly. You should just get a single executable, simply named `raxml`, which you can run for small studies and small datasets. Unfortunately, this website is *not* the top hit in Google, nor is it very easy to find from the main RAxML webpage! 

## RAxML on M3
The command below runs a 4-thread process on a single node:

```
module load raxml/8.2.9
raxmlHPC-PTHREADS -T 4 -f a -m GTRGAMMA -p 12345 -x 12345 -N 10 -s input_file.fasta -n output_file.txt
```

Don't forget to set the `SBATCH` parameters: 


### Commonly Specified Options
- `-m <model>` - Specifies the nucleotide substitution model to be used. The most common model is `GTRGAMMA`
- `-p <random seed>` - Sets the random seed for reproducibility.
- `-s <input_alignment_file>` - Specify the input alignment file. RAxML accepts relaxed `phy`, `phy`, or `fasta`.
- `-N <num_of_alternative_runs>` - No. of alternative runs on different starting trees.
- `-T <num_of_threads>` - No. of threads. Make sure to set this at most the number of CPUs you have on your machine, or this will suffer a massive performance drop!

### Bits and Bobs
- As with any file that will be fed into a tree-computing program, remove all brackets, colons and semi-colons from your file. 
- RAxML will automatically change many (or all?) special characters like "/", "-", and so on to underscores. 
