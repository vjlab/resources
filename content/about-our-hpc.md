# About Our HPC

## Logging In
You can remotely log in to our lab HPC usind `ssh`. On your terminal:

```
ssh your_username@130.194.248.38
```

You'll be prompted for your password, you can continue from there in the command line. 

## Sending/Retrieving Your Data
In a local terminal, send your files *from* your machine *to* the HPC using `scp`:

```
scp local/path/to/your/file your_username@130.194.248.38:destination_folder
```

To send files *from* the HPC *to* the local machine, run the following command in a local terminal:

```
scp your_username@130.194.248.38:source_folder local/path/to/file
```

## Sending a Job with `nohup`

To remotely send a job to the HPC and then disengage your local terminal (so that you can shut off your laptop while your submitted job runs on the HPC), use `nohup`. Syntax is:

```
nohup some_command &> my_filename.out&
```

If you don't specify the name of an output file (in the example above, `my_filename.out`, any screen output will be written to a file, `nohup.out`, by default. Note that in the event of simultaneous runs where you didn't specify a file name, output from different runs would be written to the *same* `nohup.out` file, which would just make an incredible mess of things. BEAST and RAXML runs write out their own log files, so that's not that big an issue, but their screen output (that we admittedly don't use for downstream analyses) would be printed out to the same `nohup.out` file. Your own python jobs, however, will write any `print` or `sys.out` output to the `nohup` output file. 

For instance, a standard raxml use-case would look something like:

```
nohup raxmlHPC-PTHREADS-SSE3 -T 8 -n input.fas -s output &> raxml.out&
```

Note that the `output` prefix specified by the `-s` flag is part of the `raxml` command itself. The last term, `raxml.out`, will contain all the stuff that would normally get printed on screen (a.k.a. the STDOUT).

*If none of this works, you can still walk over to the server and just use the terminal. If this is the case, do not log off after you're done; instead let it return to the "switch user" screen by itself, or your process will be stopped. This is because Linux sends a kill signal which stops all non-background processes if a user manually logs out. That's the point of `nohup` - to deliberately designate your job as a background processes.*

To connect to our server outside of the campus wifi, use a VPN (I haven't actually tried this yet). Try the **Cisco AnyConnect Secure Mobility Client** that should be available on your work laptop. 

### Killing a Job
Be careful with this, because this is a security-risk where users could accidentally kill a process other than their job. 

Use `top` to bring up a list of processes. Stop the selected process with `kill -9 <PID>`.
Ref:https://stackoverflow.com/questions/17385794/how-to-get-the-process-id-to-kill-a-nohup-process
 
