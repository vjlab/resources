# SBATCH --mail-type=FAIL

module load python/3.5.2-gcc5
python helloworld.py
```

And in the M3 terminal, I enter the following command to submit the job:

`sbatch helloworld.sh`

(Note that I'm submitting the `.sh` file, which is the *SLURM script*.  The `.py` file is a `python` script.

### BEAST Example
We usually run BEAST either using the graphical user-interface (GUI), or on the command line.  For instance, to run BEAST on our local machine, we'd use:

`beast beagle_CPU my_input_file.xml`

To interpret that: `beast` tells the terminal to do something doing BEAST, `beagle_CPU` tells the terminal to use the BEAGLE library if it's available (which it should be on the HPC), and `my_input_file.xml` is, obviously, the input file to run BEAST, in `.xml` format.

(To try this out, you can download dummy data from BEAST, called `benchmark1.xml` and `benchmark2.xml`, from their [benchmark webpage](http://beast.bio.ed.ac.uk/benchmarks).  We know the output of these datasets, so these are used to gauge the speed of different hardware setups, so that people can publish their running results with different configurations, e.g. number of CPUs, number of GPUs, etc.)

This isn't a script (like python), this is just a command on the terminal. To tell SLURM to run such commands, we use `srun`.  So, to run BEAST in SLURM, we insert the `srun` command at the bottom of our SLURM script, which I named `beast_bm1_cpu.sh`, like so:

```#!/bin/bash
Usage: sbatch beast_bm1_cpu.sh

# SBATCH --job-name=beast_bm1

# SBATCH --ntasks=1
# SBATCH --ntasks-per-node=1
# SBATCH --cpus-per-task=2

# SBATCH --time=0-01:00:00

# SBATCH --mail-user=don.teng@monash.edu
# SBATCH --mail-type=END
# SBATCH --mail-type=FAIL

# Set the file for output
# SBATCH --output=beast_bm1-%j.out

# Set the file for error log
# SBATCH --error=beast_bm1-%j.err

module load beast1/1.8.4
module load beagle
srun beast beagle_CPU benchmark1.xml
```

### RAxML Example
WIP

### Pro-Tips
- I keep my job names short (less than 10 characters long) and serializable. It also helps to keep a spreadsheet of what jobs you ran, their job IDs, when you ran them, and so on.  As the number of scripts you send increases, tracking which `.out` file came from which task can become tricky.
- To copy files from your local machine to your account on the HPC, you can use [Cyberduck](https://cyberduck.io/?l=en) or [FileZilla](https://filezilla-project.org/) GUIs (Cyberduck is recommended by the M3 admins). Otherwise, you can also use the `scp` (secure copy) command in your terminal like so:

`scp path\to\file\on\your\machine your_username:m3.massive.org.au:folder\on\massive`
