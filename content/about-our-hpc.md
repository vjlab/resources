# About Our HPC

## Temporary Note from Admin
*Our server is 90% nicely set up, but in the meantime, if you have a BEAST1 or RAxML run, do it twice: send it to the M3, and do it on our own HPC. This is because I've used M3 quite a bit for BEAST1 runs already, so I've already ironed out many the kinks with them about like getting beagle libraries to work, installing required peripheral software, etc. On the other hand, our server hasn't been field tested yet, so I expect many, many errors just to get an ordinary production run going.*

*By doing runs on both M3 and our own server, I'll also get to compare which machine is faster. From my own tests (only 1 or 2 of them so far), our server's faster. :D*

## Logging In
You can remotely log in to our lab HPC usind `ssh`. On your terminal:

```
ssh your_username@130.194.248.38
```

You'll be prompted for your password, you can continue from there in the command line. Currently, I've set up the HPC to be a purely production-level computation machine, so you can only (and need only) run large computational runs, such as for RAXML and BEAST, on it. As such, you should only need to interact with it via the command line. 

## Software, and Using the Command Line

Software available are:
- BEAST (executable `beast-mcmc`)
- RAXML (executable `raxmlHPC`, `raxmlHPC-PTHREADS` and `raxmlHPC-PTHREADS-SSE3`, in increasing order of speed; though the last two may vary)
- PHYML
- BEAGLE library

Coming up:
- BEAST2

### Sending a Job
*If none of this works, you can still walk over to the server and just use the terminal.* 

*If you're doing a computational job on the server, do not log off after you're done; instead let it return to the "switch user" screen by itself, or your process will be stopped. I think this is because Linux sends a kill signal which stops all non-background processes if a user manually logs out. That's the point of `nohup` - to deliberately designate your job as a background processes.*

To remotely send a job to the HPC and then disengage your local terminal (so that you can shut off your laptop while your submitted job runs on the HPC), use `nohup`. Syntax is:

```
nohup some_command &> my_filename.out&
```

If you don't specify the name of an output file (in the example above, `my_filename.out`, any screen output will be written to a file, `nohup.out`, by default. Note that in the event of simultaneous runs where you didn't specify a file name, output from different runs would be written to the *same* `nohup.out` file, which would just make an incredible mess of things. However, in my own tests, BEAST and RAXML runs write out their own log files anyway, so that's not that big an issue. Your own python jobs, however, will write any `print` or `sys.out` output to the `nohup` output file. 

For instance, I have a python script called `epi_search.py`, which takes in two file names as input: `input1` and `input2`. I'd run:

```
nohup python3 epi_search.py input1 input2 &
```

And press `Enter` after that.

*Admin Note* - the executables live in `/opt/`. They ought to live in `/usr/local/`.

To connect to our server outside of the campus wifi, use a VPN (I haven't actually tried this yet). Try the **Cisco AnyConnect Secure Mobility Client** that should be available on your work laptop. 

### Killing a Job
I'm disallowing this at the moment, because this is a security-risk where users could accidentally kill a process other than their job. 

For admins: use `top` to bring up a list of processes. Stop the selected process with `kill -9 <PID>`.
Ref:https://stackoverflow.com/questions/17385794/how-to-get-the-process-id-to-kill-a-nohup-process

## Retrieving Your Data
Send your files *from* your machine *to* the HPC using `scp`:

```
scp path/to/your/file your_username@130.194.248.38:destination_folder
```

Unfortunately, the only way to retrieve your data is to physically walk over, and upload the data to Google drive and send it to yourself somehow. Solutions like `scp`, or file-sharing applications like Cyberduck wcan't work unless you set up *your* own laptop to be a server, which would be a whole can of worms involving messing with firewalls and security permissions and such. 

## Performance

Performance note: all these tests were done when I was the only one using the server, so there's no additional load from someone else's job! It's possible that if two people submit their jobs simultaneously, both their jobs will be slowed down. 

- **Python3** - about 5-10% faster than M3 or my own Macbook Pro, on a single-CPU, single-thread run. 
- **RAxML** - untested
- **BEAST & BEAGLE** - untested

## Admin Notes

### Software Available:
 - R studio v0.99(ish), R v 3.4.1
 - Python 3, with the Anaconda distribution installed. Conda environment set up: access using `source activate py36`. Access `Jupyter` using `Jupyter notebook`. 
 - NVIDIA has a python library for GPU-enhanced computation: https://developer.nvidia.com/how-to-cuda-python
 
