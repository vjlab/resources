# RAxML (WIP)
*Don Teng, 6 June 2017*

Requirements: `m3-quickstart` tutorial.

## Introduction
`RAxML` takes a `.fasta` or `.txt` file of aligned sequences as input, and computes maximum likelihood trees. 

## Installation
Installing raxml on your personal computer is optional, because it's available on M3, and raxml is usually extremely slow. There are two installation options:
1. Via `homebrew`
2. Go straight [here](http://www.sfu.ca/biology2/staff/dc/raxml/), and follow their steps accordingly. That website gives you the `raxml` executable to download, simply named `raxml`, which you can run for (very) small datasets. Unfortunately, this website is *not* the top hit in Google, nor is it very easy to find from the main RAxML webpage! You'll also have to add this executable to your `PATH`, or have to run it from whichever folder you're keeping it in.

## RAxML on M3
The partial SLURM script below runs a 8-thread process on a single node, using PTHREADs for parrallelization and with SSE enabled (doesn't matter if you don't know what those are):

```
module load raxml/8.2.9
raxmlHPC-PTHREADS-SSE3 -T 8 -f a -m GTRGAMMA -p 12345 -x 12345 -N 10 -s input_file.fasta -n output_file.txt
```

The important SLURM `#SBATCH` parameters to set are:

```
#SBATCH --ntasks=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=8
#SBATCH --mem-per-cpu=10000
```

This specifies the job to run as one process (`ntask=1`), issued to a single node, and requests 8 CPUs from that node. 

### Commonly Specified RAXML Options
To see a full list of options and their explanations, use `ramxml -help`. 
- `-m <model>` - Specifies the nucleotide substitution model to be used. The most common model is `GTRGAMMA`.
- `-f <algorithm>` - Specifies the tree-computing algorithm to use; this is a bit of a black box. For most cases, we use `-f a`, to do "rapid Bootstrap analysis and search for best-scoring ML tree in one program run" (from `raxml -help`), simply because it purports to be the fastest ("rapid"). 
- `-p <random seed>` - Sets the random seed for reproducibility.
- `-s <input_alignment_file>` - Specify the input alignment file. RAxML accepts relaxed `phy`, `phy`, or `fasta`.
- `-N <num_of_alternative_runs>` - No. of alternative runs on different starting trees.
- `-T <num_of_threads>` - No. of threads. Make sure to set this at most the number of CPUs you have on your machine, or this will suffer a massive performance drop!

From previous tests (see next section), the command given above has been optimized for speed for *most* cases. Don't forget to:
- Change the number of alternative runs `-N` as required. Publication-standard is at least 100. 
- For number of threads `-T`, anywhere between 4 and 16 is a good number. Note that it's not always the more the merrier - with SSE enabled in particular, the computational cost of managing more and more CPUs will start to exceed any time savings gained from using more CPUs. 

## Performance Tests
Conducted some speed tests on M3 using 50 randomly selected Flu B Yam HA sequences, all with beagle-GPU activated. Results:

| Run               | basic   |   SSE   |   AVX   |
| ----------------- | ------- | ------- | ------- |
| 1 process, 1 CPU  | ...     | 3:44:30 | ...     |
| 1 process, 4 CPU  | 1:41:55 | 1:05:47 | 1:04:56 |
| 1 process, 8 CPU  | 0:53:32 | 0:40:38 | 0:59:47 |
| 1 process, 16 CPU | 0:48:43 | 0:48:48 | 0:59:52 |

Looks like the best bet is to go with 1-process, 8-CPU with PTHREADS-SSE. As noted in the RAxML documentation, performance does not necessarily decrease as the number of CPUs increases, as communication overhead between CPUs would increase as well. This will differ from dataset to dataset, but hopefully not by much.

### Bits and Bobs
- As with any file that will be fed into a tree-computing program, remove all brackets, colons and semi-colons from your file. 
- RAxML will automatically change many (or all?) special characters like "/", "-", and so on to underscores. 
