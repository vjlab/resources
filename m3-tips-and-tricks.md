# M3 Tips and Tricks
### Frequently Used HPC Commands

| Command                          | Description         | 
| -------------------------------- | ------------- | 
| `squeue`                         | View all jobs currently being run on the HPC                    |
| `squeue --user=<your_username>`  | View just the jobs that you're running                          |
| `show_cluster`                   | Check the availability of different nodes                       |
| `mkdir <name_of_new_folder>`     | Create a new folder                                             |
| `ls`                             | See what files there are in the folder that you're currently in |
| `ls -G`                          | Same as `ls`, but with colour-coding by file type               |
| `nano my_file`                   | To view or edit `my_file`                                       |
| `rm file_to_delete               | Delete a file                                                   |

You can alias all these commands to prevent yourself from having to type long commands over and over again. Access and modify your `bash_profile` using:

`nano ~/.bash_profile`

And add an alias like:

`alias qu="squeue --user=<your_username>`

### Running the same command on multiple files.
Say I wish to perform the same MSA on several `fasta` files. That is, I'd like to run:

`mafft input.fasta > output.fasta`

A typical example is doing multiple-sequence alignment on all eight gene segments of a flu virus, which exist as eight `.fasta` files.

You can create a text file with a list of bash commands, and run them all one after another by calling the `bash` command on that text file. For instance, create a file `my_run.txt`, containing the following:

```
echo "first command"
echo "second command"
date
```

And in your terminal, cd to the place where you've saved `my_run.txt` and do:

`bash my_run.txt`

This will print out "first command", "second command", and today's date.

Similarly, you can prepare a `msa_run.txt` file like:

```
mafft input1.fasta > output1.fasta
mafft input2.fasta > output2.fasta
mafft input3.fasta > output3.fasta
```

And a SLURM script like:

```
SBATCH...
...
module load mafft/7.310
bash
```

Upload the fasta files, the run text file and the SLURM script onto M3, and submit the SLURM job as usual
