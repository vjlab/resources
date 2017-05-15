# M3 High-Performance Computing (HPC) Quickstart (WIP)
*Don Teng, 28 April 2017*

Level: Beginner

1. Introduction
2. Logging into M3
3. Running a SLURM Script in M3
4. Uploading/Downloading files
5. Tips

## 1. Introduction
A generic *programming script* is a text file containing a list of instructions for a computer to carry out. The computer must be given instructions in a very specific format that it can understand.

M3 is the high-performance computing (HPC) resource provided by Monash. It's like having a second very, very powerful computer (actually *computers*), but you can't easily interact with it with point-and-click interface. You have to tell it what to do by preparing a list of instructions, called a *SLURM script*. Note that "HPC" and "M3" will be used interchangeably where context is clear, where "M3" is actually the *name* of Monash Uni HPC resource.

[SLURM](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) is a queueing manager used by many HPCs around the world; widely used because it's open-source (i.e. free). It's necessary because there are often multiple users requesting computational resources from the same HPC, with different computational demands, runtimes, and so on.  So SLURM doesn't actually do any computation, it assigns user-submitted computing tasks to the nodes within the HPC cluster as efficiently as possible.

As a practical for this tutorial, it's recommended that you do a dummy run of the BEAST software - no knowledge of BEAST is required. Download a data input file `benchmark1.xml` from [here](https://github.com/beast-dev/beast-mcmc/blob/master/examples/release/Benchmarks/benchmark1.xml) - this file contains the raw data and some parameters in a format that BEAST understands. In this practical, you'll:
1. Prepare a SLURM script, using the template provided
2. Submit the SLURM script to the HPC, telling the HPC to run a BEAST command
3. Retrieve the output of your HPC job.

## 2. Logging into M3
Open your Terminal (assuming you're using a Mac), and in the command line, login using:

`$ ssh <your_username>@m3.massive.org.au`

You'll be prompted for your password, and then you're in.

## 3. Running a Command in M3
M3 needs two kinds of information:
1. Specifics of your HPC computational needs like number of nodes, number of cores per node, memory usage, runtime etc.
2. The actual job that needs to be run, e.g. a command like `beast -beagle_off my_input_file.xml`

Finding out how to specify (1) can be tricky; but you can use the default settings specified below for most cases. (2) needs to be modified depending on what program you're running. The example SLURM script below will do a BEAST run using the `benchmark1.xml` file downloaded earlier. On your own computer, create a new SLURM script by copying and pasting the text below into a new text file, and save that textfile as `my_slurm_script.txt`. Only your email needs to be modified at the line `#SBATCH --mail-user=<your_email>`.

`#!/bin/bash

#SBATCH --job-name=my_job

#SBATCH --ntasks=1
#SBATCH --ntasks-per-node=1

#SBATCH --time=0-02:00:00

#SBATCH --mail-user=<your_email>
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL

module load beast1/1.8.4
module load beagle
beast -beagle_off benchmark1.xml`

To break that down:
 - The very first line `#!/bin/bash` tells the HPC that this file is a list of instructions, not just a bunch of text. Always include it in the first line of your SLURM scripts.
 - All the lines starting with `#SBATCH` are *run parameters*, e.g. run time, number of CPUs you'd like to request, etc.
 - The lines at the bottom: `module load...`, `beast...` are the actual BEAST command lines. That is, if you have BEAST on your own computer, you'd run this same computation using `beast -beagle_off benchmark1.xml` on your own command line. 

The run parameters that have been specified in this example are chosen because you'll probably only need to work with these:
 - #SBATCH --job-name=my_job - Name of job that appears in the queue: `my_job`
 - #SBATCH --time=0-02:00:00 - Run time requested: 2h. 
 - #SBATCH --ntasks=1... - Request only one node. Don't worry if you don't know what this means.
 - #SBATCH --mail-user=<your_email>... - Request SLURM to send you an email when the job is completed, or terminated with an error.

After logging onto M3, submit a script to the queue by entering, in the command line:

`$ sbatch my_slurm_script.sh`

You should recieve a message containing a job ID:

`Submitted job 1234`

It usually takes a second to submit your script to the queue.

Note that if you don't see your script in the queue, two things could have happened: 1. your script still hasn't been submitted yet, or 2. your script terminated almost instantaneously with an error, and therefore appeared in and then disappeared from the queue within microseconds. To check the second scenario, check if there's a slurm output file in your directory. You can also tell SLURM to send you an email whenever the job ends, whether it ended successfully, or with an error.

## 4. Uploading/Downloading Files
I recommend [Cyberduck](https://cyberduck.io/?l=en) as a user interface to easily upload and download files from M3; it's as easy as drag-and-drop. On the Cyberduck interface:



## 5. Frequently Used M3 Commands
To view all jobs currently being run:

`squeue`

An output file named something like `slurm-<job ID>.out` containing all the relevant output will be automatically created in your M3 folder.  To view (or edit) this file, use the `nano` command:

`nano slurm-1234.out`

To copy files from your local machine to your account on the HPC, you can use [Cyberduck](https://cyberduck.io/?l=en) or [FileZilla](https://filezilla-project.org/) GUIs (Cyberduck is recommended by the M3 admins). You can also use the `scp` (secure copy) command in your terminal like so:

`scp path\to\file\on\your\machine your_username:m3.massive.org.au:folder\on\massive`

## 6. Tips
 - Read the manual [here](http://docs.massive.org.au/M3/slurm/slurm-overview.html)
 - Troubleshooting your job in M3 can be especially tricky, because now you have the additional layer of complexity where you're telling the HPC what you want to run.  If something goes wrong, the error could be with the HPC, or maybe the SLURM script was wrongly specified, or in your program. It's good practice to do a short test run first before doing a full-length run.
