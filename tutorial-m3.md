# Writing Scripts for M3
*Don Teng, 3 April 2017*

1. What is a Script?
2. Preparing a Script for SLURM
3. Running a Script in M3
4. Tips

## 1. What is a Script?
A generic *programming script* is a text file containing a list of instructions for a computer to carry out. The computer must be given instructions in a very specific format that it can understand, so it's a bit of work to set up a script.

## 2. Preparing a Script for SLURM
[SLURM](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) is a queueing manager used by many HPCs around the world; widely used because it's open-source (i.e. free). It doesn't actually do any computation, it assigns user-submitted computing tasks to the nodes within a computing cluster as efficiently as possible, so everyone gets their computational needs met.

You can submit the following information (* = essential):
- **Job name***, which will be shown in the queue. 
- **Number of tasks.*** The number of tasks that can be done in parrallel. 
- **Number of tasks per node**.*
- **CPUs per task**.* This can be kept at 1.
- **Running time**.* The maximum amount of time that you want your script to run for. 
- **Memory per CPU**. Unless you set this to a very small number (like 10), this doesn't appear to make much difference.
- **Your email**, so that you can be notified when a job finishes.

To find the required information, SLURM looks for an `# SBATCH` in front of these options. For intance, to tell SLURM your job name:

`# SBATCH --job-name=MyJob`

A full example of how to enter the other bits of information can be found in example scripts on your M3 account. Also, the Victorian Life Sciences Computation Initiative (VLSCI) has a handy web form for you to fill this all in, and generates a script for you. 

In order to actually tell SLURM what you want computed, you'll have to write either a separate script, or enter a command as you would on the terminal of your own machine. A few examples of these are available below.

## 3. Running a Script in M3
You can submit a script by connecting to M3, and entering, in the command line:

`$ sbatch my_slurm_script.sh`

You'll be given a job ID. You should recieve a message like:

`Submitted job 1234`

Where 1234 is your job ID. It usually takes a second to submit your script to the queueing manager. To view all jobs currently being run:

`squeue`

An output file named something like `slurm-<job ID>.out` containing all the relevant output will be automatically created in your M3 folder.  To view this file, use the `nano` command:

`nano slurm-1234.out`

For instance, in our earlier Hello World example, the "Hello world" would have been printed in this `.out` file.

Note that if you don't see your script in the queue, two things could have happened: 1. your script still hasn't been submitted yet, or 2. your script terminated almost instantaneously with an error, and therefore appeared in and then disappeared from the queue within microseconds. To check the second scenario, check if there's a slurm output file in your directory. 

### Python "Hello World" Example
*Note: at the time of this writing, Python doesn't quite work yet; still working with the folks at M3 to fix this.*

For instance, let's say that I want to just print "Hello world", using `python`. I'll create a simple `python` script, say, `helloworld.py`, which contains just the single line:

`print("Hello world!")`

And another separate SLURM script, `helloworld.sh`, which looks like:
```
#!/bin/bash

# SBATCH --job-name=helloworld

# SBATCH --ntasks=1
# SBATCH --ntasks-per-node=1
# SBATCH --cpus-per-task=1

# SBATCH --time=0-01:00:00

# SBATCH --mail-user=don.teng@monash.edu
# SBATCH --mail-type=END
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

### 4. Tips
- I keep my job names short (less than 10 characters long) and serializable. It also helps to keep a spreadsheet of what jobs you ran, their job IDs, when you ran them, and so on.  As the number of scripts you send increases, tracking which `.out` file came from which task can become tricky.
- To copy files from your local machine to your account on the HPC, you can use [Cyberduck](https://cyberduck.io/?l=en) or [FileZilla](https://filezilla-project.org/) GUIs (Cyberduck is recommended by the M3 admins). Otherwise, you can also use the `scp` (secure copy) command in your terminal like so:

`scp path\to\file\on\your\machine your_username:m3.massive.org.au:folder\on\massive`
