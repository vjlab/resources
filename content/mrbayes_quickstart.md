# MrBayes Quickstart Tutorial

(Mostly a condensed verion of the quickstart already in the official manual, or the Wiki. Tested using `mrbayes` on a Linux machine.)

## Overview

* Uses a variant of MCMC (with "hot" and "cold" chains - see the **MCMC Chains** section below) to produce a file with multiple trees <extension `.t`). Does not produce time-resolved trees.
* Pretty fast for an MCMC-based tree algorithm (faster than BEAST, anyway).
* Can do other kinds of analysis like dNdS, with HPD intervals.
* Doesn't like special characters - will convert them all to underscores. This is highly annoying.

## Quickstart
### 1. Prepare a `.nexus` File

### 2. Basic Commands

Prepare a `run.txt` file with the following lines:

```
begin mrbayes;
    set autoclose=yes;
    set usebeagle=yes beagledevice=gpu beagleprecision=single;
    execute input_file.nexus;
    lset nst=6 rates=gamma;
    mcmc nruns=1 nchains=2 ngen=10000000 samplefreq=10000 printfreq=10000 diagnfreq=100000;
end;
```

To break that down:
* `set autoclose=yes` - prevents the program from prompting during the run. In interactive mode, `mrbayes` will ask to confirm whether or not to continue with the run very 20,000 generations.
* `set usebeagle=yes beagledevice=gpu beagleprecision=single;` - Use the BEAGLE GPU library. Use single-precision for less accurate, but marginally faster runs. There's a BEAGLE SSE option as well, which doesn't help with single-precision runs, but could help speed up double-precision runs (not tested yet)
* `execute input_file.nexus;` - Loads the input file, in nexus format.
* `lset nst=6 rates=gamma;`

### 3. Run Batch File with `nohup`


### MCMC Chains [1]

MrBayes runs a _Metropolis-coupled Markov Chain Monte Carlo_ algorithm, or MCMCMC. This is to solve a practical problem where the target distribution has multiple peaks, separated by valleys. Instead of 1 MCMC robot (as with BEAST), we have, say, 4 robots (default `mrbayes` setting: 3 "hot" chains, 1 "cold" chain), exploring the landscape in parallel. At the end of the run, only the output from the cold chain is kept; the rest are discarded.

* The "cold" chain is the "main" chain, and behaves as normal (like in BEAST)
* The "hot" chains have a flatter distribution, which makes it easier for them to avoid getting stuck in valleys or local peaks.
* Every so often, a "cold" chain may swap with a "hot" chain. This allows cold chains to "jump" through valleys easier.

But because there are more MCMC chains running at the same time, runtime is will be multiplied by the number of chains running. At present, I'm making a cautious recommendation of at most 2 chains, because I haven't been able to test whether more chains is actually better (or, will they lead to at least 4x better mixing?)

## MPI runs

### Compiling the MPI version

You'll need (all already available in our server):

* `gcc` (or some other C compiler)
* `autotools` (for `autoconf`)
* `mpicc` for MPI compiler
* `BEAGLE` library

Download MrBayes from source, cd into the `/src` directory, and execute the following commands:

```
autoconf
./configure --enable-mpi=yes
make
```

This will create an executable named `mb`.

### Running MPI

As far as I know, this an only be done in batch mode. Simply run:

```
mpirun -np 2 mb my_nexus_file.nex
```

This will use both cores (`-np 2`) of our server.

## Useful Links

* [1] [Wikipedia article](https://en.wikipedia.org/wiki/Bayesian_inference_in_phylogeny) on MCMCMC
* Tim Vaughan's Bayesian MCMC [lecture slides](https://tgvaughan.github.io/BayesianMCMCLectures/)
