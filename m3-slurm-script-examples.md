# M3 Example SLURM Scripts

### 1. BEAST Example
BEAST is a bit of software which computes phylogenetic trees within a Bayesian statistical framework (that's what the "B" in 'BEAST' stands for).  It accepts as input an `xml` file in a specific format (you can use `BEAUTI` to create this format), and returns a phylogenetic tree (a `.tree` file) and a couple of other secondary output files like a log file. We usually run BEAST either using the graphical user-interface (GUI), or on the command line.  For instance, to run BEAST on our local machine, we'd use something like:

`beast -beagle_CPU my_input_file.xml`

To interpret that: `beast` tells the terminal to do something doing BEAST, `-beagle_CPU` tells the terminal to use the BEAGLE library if it's available (which it should be on the HPC), and `my_input_file.xml` is, obviously, the input file to run BEAST, in `.xml` format.

(To try this out, you can download dummy data from BEAST, called `benchmark1.xml` and `benchmark2.xml`, from their [benchmark webpage](http://beast.bio.ed.ac.uk/benchmarks).  We know the output of these datasets, so these are used to gauge the speed of different hardware setups, so that people can publish their running results with different configurations, e.g. number of CPUs, number of GPUs, etc.)

The SLURM script is as follows::

```#!/bin/bash
Usage: sbatch beast_bm1_cpu.sh

#SBATCH --job-name=beast_bm1

#SBATCH --ntasks=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1

#SBATCH --time=0-01:00:00

#SBATCH --mail-user=don.teng@monash.edu
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL

module load beast1/1.8.4
module load beagle
beast -beagle_CPU benchmark1.xml
```

### 1b. BEAST BEAGLE with the GPU
The BEAGLE library is a helper program to BEAST to speed up computations. It can do this in a few ways - this section tells you how to utilize the GPU. 

(A *CPU* is the "normal" kind of processing unit present in all computers. A Graphical-Processing-Unit (GPU) is an additional bit of hardware, popular amongst gamers because computer games require extremely powerful processing units capable of rendering 3D environments.)

The computers (or "nodes") on the HPC that have GPUs are in the partition m3c and m3f. Aside from the usual `#SBATCH` parameters specified above, you'll have to include a couple more `#SBATCH` lines. The run command is also quite different:

```
#SBATCH --gres=gpu:1
#SBATCH --partition=m3c

module load beast1/1.8.4
module load beagle/2.1.2
module switch cuda/7.0

beast -beagle_info
beast -beagle_cuda -beagle_order 1,0 benchmark1.xml
```

*Coming soon: -beagle_SSE*

### 2. RAxML Example
RAxML is the trickiest to use because tweaking RAXML for optimal speed is a [giant can of worms](https://sco.h-its.org/exelixis/resource/download/NewManual.pdf).  The example given below is not optimized for speed for most applications - in particular, run time increases exponentially as the number and length of sequences increases - but it should do just to get things running first. RaxML wasn't written to utilize GPUs, so don't bother sending your job to GPU partitions.

A "default" run command is:

```
...
#SBATCH --ntasks=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=4
...

raxmlHPC-PTHREADS -T 4 -f a -m GTRGAMMA -p 12345 -x 12345 -N 200 -s input_file.fasta -n output_file.txt
```

That is: this job is split into 4 processes, which get distributed to 4 CPU cores in 1 node. Anecdotally, from my own runs, choose 2 to 8 threads for best results; any more than that would just slow down the run with increased communication overhead between that many cores. 

### 3. Python "Hello World" Example
For instance, let's say that I want to print "Hello world", using `python`. I'll create a simple `python` script, say, `helloworld.py`, which contains just the single line:

`print("Hello world!")`

And another separate SLURM script, `helloworld.sh`, which looks like:
```
#!/bin/bash

#SBATCH --job-name=helloworld

#SBATCH --ntasks=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1

#SBATCH --time=0-01:00:00

#SBATCH --mail-user=don.teng@monash.edu
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL

module load python/3.5.2-gcc5
python3 helloworld.py
```https://github.com/vjlab/resources/blob/master/m3-slurm-script-examples.md

And in the M3 terminal, I enter the following command to submit the job:

`sbatch helloworld.sh`

(Note that I'm submitting the `.sh` file, which is the *SLURM script*.  The `.py` file is a `python` script.
