# MrBayes Quickstart Tutorial

_(Mostly a condensed verion of the quickstart already in the official manual, or the Wiki. Tested using `mrbayes` on a Linux machine.)_

### Overview

* Uses a variant of MCMC (with "hot" and "cold" chains - see the **MCMC Chains** section below) to produce a file with multiple trees <extension `.t`). Does not produce time-resolved trees.
* Pretty fast for an MCMC-based tree algorithm (faster than BEAST, anyway).
* Can do other kinds of analysis like dNdS, with HPD intervals.
* Doesn't like special characters - will convert them all to underscores. This is highly annoying.

## 1. Quickstart

There are two modes of operation: interactive mode and batch mode. The interactive mode is initialized just by typing `mb` into the command line, after which you'll enter parameter inputs line by line, and in batch mode, you'll prepare a text file containing all the necessary parameters, and simply run that text file with `mb my_run_file.txt`. This tutorial assumes that you already have a suitable input `.nexus` file containing your aligned sequences. 

### Interactive mode

Initialize with `mb`, then enter the following lines:

```
set usebeagle=yes beagledevice=gpu beagleprecision=single;
execute input_file.nexus;
lset nst=6 rates=gamma;
mcmc nruns=1 nchains=2 ngen=10000000 samplefreq=10000 printfreq=10000 diagnfreq=100000;
```

To break that down:
* `set usebeagle=yes beagledevice=gpu beagleprecision=single;` - Use the BEAGLE GPU library. Use single-precision for less accurate, but marginally faster runs. There's a BEAGLE SSE option as well, which doesn't help with single-precision runs, but could help speed up double-precision runs (not tested yet)
* `execute input_file.nexus;` - Loads the input file, in nexus format.
* `lset nst=6 rates=gamma;`- Use the GTR model, with gamma priors. Use `help lset` in interactive mode to see more options. 

### Batch mode

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

The additional `set autoclose=yes` line prevents the program from prompting during the run. In interactive mode, `mrbayes` will ask to confirm whether or not to continue with the run very 20,000 generations; the `autoclose` flag switches off that behaviour. 

Run the batch mode file with `nohup`:

```
nohup mb run.txt &> log.out&
```

This will write all screen output (STDOUT) to `log.out`. 

## 2. Advanced Usage with MPI

_Stick to the single-core use first, because, oddly, mpi slows down, rather than speeds up, `mrbayes` jobs with multiple runs and/or chains. I suspect that mpicc just hasn't been tweaked properly yet, or I mucked up the mpi-enabled compilation somewhere. This section is here just for your interest._

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

## 3. More Useful Stuff

### MCMC Chains[1]

MrBayes runs a _Metropolis-coupled Markov Chain Monte Carlo_ algorithm, or MCMCMC. This is to solve a practical problem where the target distribution has multiple peaks, separated by valleys. Instead of 1 MCMC robot (as with BEAST), we have, say, 4 robots (default `mrbayes` setting: 3 "hot" chains, 1 "cold" chain), exploring the landscape in parallel. At the end of the run, only the output from the cold chain is kept; the rest are discarded.

* The "cold" chain is the "main" chain, and behaves as normal (like in BEAST)
* The "hot" chains have a flatter distribution, which makes it easier for them to avoid getting stuck in valleys or local peaks.
* Every so often, a "cold" chain may swap with a "hot" chain. This allows cold chains to "jump" through valleys easier.

The default setting for `mrbayes` is to have 2 runs, each with 4 chains (3 hot, 1 cold). I recommend using 1 run with 2 chains, because:

* Total runtime is presently still a multiple of the number of runs and number of chains. If 1 run with 1 chain takes 1 hour, then 1 run with 2 chains takes 2 hours, and 2 runs, each with 4 chains, would take 8 hours. 
* **Number of chains*** - It's difficult to ascertain the optimal number of chains - 4 chains does not garauntee 4x better MCMC mixing. Mixing, after all, is ultimately dependant on the dataset. So for now, 2 chains is the best strategy that minimally utilizes the chain-swapping feature. 
* **Number of runs** - On our server, increasing the number of runs will just slow down total compute time by a multiple of however many runs were started. So might as well initialize reruns as necessary, instead of asking for 3 runs at once. 

### Useful Links

* [1] [Wikipedia article](https://en.wikipedia.org/wiki/Bayesian_inference_in_phylogeny) on MCMCMC
* Tim Vaughan's Bayesian MCMC [lecture slides](https://tgvaughan.github.io/BayesianMCMCLectures/)
