# M3 High-Performance Computing (HPC) Quickstart (WIP)
*Don Teng*

*Last update 16 May 2017*

Level: Beginner
See also: the Cyberduck tutorial.

In this tutorial, we're going to practice doing a BEAST run on the HPC. The BEAST software computes evolutionary trees from input sequence data, but no knowledge of the BEAST software is required in this tutorial.  We're going to:
 - Prepare a SLURM script, `my_slurm_script.txt` - a bunch of instructions that tells the HPC what to do
 - Get an `xml` file, `benchmark1.xml` - a bunch of instructions that tells the BEAST software what to do. Download it [here](https://github.com/beast-dev/beast-mcmc/blob/master/examples/release/Benchmarks/benchmark1.xml) - this file contains the raw data and some parameters in a format that BEAST understands. 
 - Upload both files to the HPC (see the Cyberduck tutorial)
 - Submit the SLURM script (or "submit the job") to the HPC, and review a bunch of frequently used HPC commands
 - Retrieve your job output after the run is complete.

## 1. Introduction
A generic *programming script* is a text file containing a list of instructions for a computer to carry out. The computer must be given instructions in a very specific format that it can understand.

M3 is the high-performance computing (HPC) resource provided by Monash. It's like having a second very, very powerful computer (actually *computers*), but you can't easily interact with it with a point-and-click interface. You have to tell it what to do by preparing a list of instructions, called a *SLURM script*. Note that "HPC" and "M3" will be used interchangeably where context is clear, where "M3" is actually the *name* of Monash Uni HPC resource.

[SLURM](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) is a queueing manager used by many HPCs around the world; widely used because it's open-source (i.e. free). It's necessary because there are often multiple users requesting computational resources from the same HPC, with different computational requirements, runtimes, and so on.  So SLURM doesn't actually do any computation, it assigns user-submitted computing tasks to the nodes within the HPC cluster as efficiently as possible.

## 3. Writing a SLURM Script
M3 needs two kinds of information:
1. Specifics of your HPC computational needs like number of nodes, number of cores per node, memory usage, runtime etc. For the purposes of this tutorial, you can just use the settings provided in the example below.
2. The actual job that needs to be run, e.g. a command like `beast -beagle_off my_input_file.xml`

The example SLURM script below will do a BEAST run using the `benchmark1.xml` file downloaded earlier. On your own computer, create a new SLURM script by copying and pasting the text below into a new text file, and save that text file as `my_slurm_script`. Make sure to enter your email at the line `#SBATCH --mail-user=<your_email>`.

```
#!/bin/bash

#SBATCH --job-name=my_job

#SBATCH --ntasks=1
#SBATCH --ntasks-per-node=1

#SBATCH --time=0-02:00:00

#SBATCH --mail-user=<your_email>
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL

module load beast1/1.8.4
module load beagle
beast -beagle_off benchmark1.xml
```

To break that down:
 - The very first line `#!/bin/bash` tells the HPC that this file is a list of instructions, not just a bunch of text. Always include it in the first line of your SLURM scripts.
 - All the lines starting with `#SBATCH` are *run parameters*, e.g. run time, number of CPUs you'd like to request, etc.
 - The lines at the bottom: `module load...`, `beast...` are the actual BEAST command lines. That is, if you have BEAST on your own computer, you'd run this same computation using `beast -beagle_off benchmark1.xml` on your own command line. 

## 2. Job Submission to M3
Open your Terminal (assuming you're using a Mac), and in the command line, login using:

```
$ ssh <your_username>@m3.massive.org.au
```

You'll be prompted for your password, and then you're in.

Upload both `my_slurm_script` and `benchmark1.xml` to your account on M3, using Cyberduck.  Now submit your script to the queue by entering, in the command line:

```
$ sbatch my_slurm_script
```

You should recieve a message containing a job ID, like:

```
Submitted job 1234
```

It usually takes a second to submit your script to the queue.

Note that if you don't see your script in the queue, two things could have happened: 1. your script still hasn't been submitted yet, or 2. your script terminated almost instantaneously with an error, and therefore appeared in and then disappeared from the queue within microseconds. To check the second scenario, check if there's a slurm output file in your directory. You can also tell SLURM to send you an email whenever the job ends, whether it ended successfully, or with an error.

## 5. Frequently Used HPC Commands
To view all jobs currently being run on the HPC:

`squeue`

To view just the jobs that you're running:

`squeue --user=<your_user_name>`

To create a new folder in your home directory:

`mkdir new_folder`

To navigate into that folder:

`cd new_folder`

To return to your main folder:

`cd`

To see what files there are in the folder that you're currently in:

`ls`

To view or edit the contents of a particular file:

`nano my_file`

To delete a file:

`rm file_to_delete`

## Reviewing your Output
All jobs that were run on the HPC will automatically generate an output file `slurm-<job_id>.out`.  This is like a text file, but, somewhat annoyingly, can't be viewed with a text editor.  You can read the contents of this file using the `nano` command:

`nano slurm-12345.out`

BEAST would have generated some other files as well, but we don't need to look at those for the purposes of this tutorial. The main BEAST output would have been recorded in the SLURM output file.

## 6. Tips
 - [Read the M3 documentation](http://docs.massive.org.au/M3/slurm/slurm-overview.html)
 - Troubleshooting your job in M3 can be especially tricky, because now you have the additional layer of complexity where you're telling the HPC what you want to run.  If something goes wrong, the error could be with the HPC, or maybe the SLURM script was wrongly specified, or in your program. It's good practice to do a short test run first before doing a full-length run.
 - To upload/download files to/from M3, you can also use the `scp` (secure copy) command in your terminal like so:

```
scp path\to\file\on\your\machine your_username:m3.massive.org.au:folder\on\massive
```
