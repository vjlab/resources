# About Our HPC

## Logging In
You can remotely log in to our lab HPC usind `ssh`. On your terminal:

```
ssh your_username@130.194.248.38
```

You'll be prompted for your password. 

You should first see a `$` symbol. Start up a terminal remotely using:

```
bash
```

And you can continue from there.

## Software, and Using the Command Line

I've only installed the heavy-duty software, i.e. only BEAST, RAxML and BEAGLE. The executables are `beast-mcmc` for beast, and `raxmlHPC`, `raxmlHPC-PTHREADS` and `raxmlHPC-PTHREADS-SSE3` for RAxML (in increasing order of speed; though the last two may vary). To send a job to the HPC and then disengage your local terminal (so that you can shut off your laptop while your submitted job runs on the HPC), use `nohup`:

```
nohup <command> <command_flag> &
```

Screen output will be written to a file, `nohup.out`. For instance, I have a python script called `epi_search.py`, which takes in two file names as input: `input1` and `input2`. I'd run:

```
nohup python3 epi_search.py input1 input2 &
```

*Admin Note* - the executables live in `/opt/`. They ought to live in `/usr/local/`.

## Performance

- **Python3** - about 5-10% faster than M3 or my own Macbook Pro, on a single-CPU, single-thread run. 
- **RAxML** - untested
- **BEAST & BEAGLE** - untested
