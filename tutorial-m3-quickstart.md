# M3 High-Performance Computing (HPC) Quickstart Guide
*Don Teng, 28 April 2017*
Level: Intermediate - rudimentary knowledge of scripting and command line required

1. Introduction
2. Logging into M3
3. Running a SLURM Script in M3
4. Uploading/Downloading files
5. Tips

## 1. Introduction
A generic *programming script* is a text file containing a list of instructions for a computer to carry out. The computer must be given instructions in a very specific format that it can understand.

M3 is the high-performance computing (HPC) resource provided by Monash. It's like having a second very, very powerful computer (actually *computers*), but you can't easily interact with it with point-and-click interface. You have to tell it what to do by preparing a list of instructions, called a *SLURM script*.

[SLURM](https://en.wikipedia.org/wiki/Slurm_Workload_Manager) is a queueing manager used by many HPCs around the world; widely used because it's open-source (i.e. free). It's necessary because there are often multiple users requesting computational resources from the same HPC, with different computational demands, runtimes, and so on.  So SLURM doesn't actually do any computation, it assigns user-submitted computing tasks to the nodes within the HPC cluster as efficiently as possible.

## 2. Logging into M3
Open your Terminal (assuming you're using a Mac), and in the command line, login using:

`$ ssh <your_username>@m3.massive.org.au`

You'll be prompted for your password, and then you're in.

## 3. Running a Script in M3
You can submit a script by connecting to M3, and entering, in the command line:

`$ sbatch my_slurm_script.sh`

You'll be given a job ID. You should recieve a message like:

`Submitted job 1234`

Where 1234 is your job ID. It usually takes a second to submit your script to the queueing manager. For instance, in our earlier Hello World example, the "Hello world" would have been printed in this `.out` file.

Note that if you don't see your script in the queue, two things could have happened: 1. your script still hasn't been submitted yet, or 2. your script terminated almost instantaneously with an error, and therefore appeared in and then disappeared from the queue within microseconds. To check the second scenario, check if there's a slurm output file in your directory. You can also tell SLURM to send you an email whenever the job ends, whether it ended successfully, or with an error.

When reading a script, SLURM looks for an `#SBATCH` in front of these options. For intance, to tell SLURM your job name:

`#SBATCH --job-name=MyJob`

A basic template for a SLURM script, `slurm-quickstart`, has been uploaded to this repo. It's ready to be run without any modification, and contains some frequently-used specifications and their default or recommended values. 

## 4. Uploading/Downloading Files
I recommend [Cyberduck](https://cyberduck.io/?l=en) as a user interface to easily upload and download files from M3; it's as easy as drag-and-drop. 

## 5. Frequently Used M3 Commands
To view all jobs currently being run:

`squeue`

An output file named something like `slurm-<job ID>.out` containing all the relevant output will be automatically created in your M3 folder.  To view this file, use the `nano` command:

`nano slurm-1234.out`

To copy files from your local machine to your account on the HPC, you can use [Cyberduck](https://cyberduck.io/?l=en) or [FileZilla](https://filezilla-project.org/) GUIs (Cyberduck is recommended by the M3 admins). Otherwise, you can also use the `scp` (secure copy) command in your terminal like so:

`scp path\to\file\on\your\machine your_username:m3.massive.org.au:folder\on\massive`

## 6. Tips
 - Read the manual [here](http://docs.massive.org.au/M3/slurm/slurm-overview.html)
 - Troubleshooting your job in M3 can be especially tricky, because now you have the additional layer of complexity where you're telling the HPC what you want to run.  If something goes wrong, the error could be with the HPC, or maybe the SLURM script was wrongly specified, or in your program. It's good practice to do a short test run on your own machine first before sending it to the HPC for a full-length run.
