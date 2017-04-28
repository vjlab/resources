# M3 High-Performance Computing (HPC) Quickstart Guide
*Don Teng, 28 April 2017*

1. Introduction
2. Preparing a SLURM Script
3. Running a SLURM Script
4. Uploading/Downloading files
5. Tips

## 1. Introduction
A generic *programming script* is a text file containing a list of instructions for a computer to carry out. The computer must be given instructions in a very specific format that it can understand.

M3 is the high-performance computing (HPC) resource provided by Monash. It's like having a second very, very powerful computer (Actually *computers*), but you can't easily interact with it with point-and-click interfaces. You have to tell it what to do by preparing a list of instructions, called a *SLURM script*.

## 2. Preparing a SLURM Script
[SLURM](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) is a queueing manager used by many HPCs around the world; widely used because it's open-source (i.e. free). It's necessary because there are often multiple users requesting computational resources from the same HPC, with different computational demands, runtimes, and so on.  So SLURM doesn't actually do any computation, it assigns user-submitted computing tasks to the nodes within the HPC cluster as efficiently as possible.

A basic template for a SLURM script is in this repo, named `slurm-quickstart`. It's ready to be run without any modification. 

When reading a script, SLURM looks for an `# SBATCH` in front of these options. For intance, to tell SLURM your job name:

`# SBATCH --job-name=MyJob`

A full example of how to enter the other bits of information can be found in example scripts on your M3 account. 

In order to actually tell SLURM what you want computed, you'll have to write either a separate script, or enter a command as you would on the terminal of your own machine. A few examples of these are available below.

## 3. Running a Script in M3
You can submit a script by connecting to M3, and entering, in the command line:

`$ sbatch my_slurm_script.sh`

You'll be given a job ID. You should recieve a message like:

`Submitted job 1234`

Where 1234 is your job ID. It usually takes a second to submit your script to the queueing manager. For instance, in our earlier Hello World example, the "Hello world" would have been printed in this `.out` file.

Note that if you don't see your script in the queue, two things could have happened: 1. your script still hasn't been submitted yet, or 2. your script terminated almost instantaneously with an error, and therefore appeared in and then disappeared from the queue within microseconds. To check the second scenario, check if there's a slurm output file in your directory. 

## 4. Uploading/Downloading Files
I recommend [Cyberduck](https://cyberduck.io/?l=en) as a user interface to easily upload and download files from M3; it's as easy as drag-and-drop. 

## 5. Frequently Used M3 Commands
To view all jobs currently being run:

`squeue`

An output file named something like `slurm-<job ID>.out` containing all the relevant output will be automatically created in your M3 folder.  To view this file, use the `nano` command:

`nano slurm-1234.out`

To copy files from your local machine to your account on the HPC, you can use [Cyberduck](https://cyberduck.io/?l=en) or [FileZilla](https://filezilla-project.org/) GUIs (Cyberduck is recommended by the M3 admins). Otherwise, you can also use the `scp` (secure copy) command in your terminal like so:

`scp path\to\file\on\your\machine your_username:m3.massive.org.au:folder\on\massive`
