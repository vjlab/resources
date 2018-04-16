# HPC & Data-serving Resources

We have two major HPC resources:

### 1. A linux box in room 217. 

* Linux Mint 18.2, xcfe
* 32x CPU (Intel Xeon E5-2667 v4, 16 physical + 16 logical threads)
* 2x GeForce 1080Ti GPU
* 64Gb RAM
* 1Tb disk space: 500 Gb `/scratch` + 500 Gb of `/data`. 

### 2. M3

* [Read the docs!](http://docs.massive.org.au/)
* In general, M3 has many (many, many) more CPUs available (n=1584), and so are ideal for extensively multi-threaded jobs (we only have 2 CPUs, with 16 threads each, and no `openMPI` advantage, because optimal thread usage for phylogenetics software tends to top out at 8 threads.)
* The M3 GPUs: K80, K1 and P100 are all optimized for single-precision performance, but any one user will only have access to 4 M3 GPU nodes. Our 1080 Ti's aren't too shabby, good for double-precision, and can sometimes run faster, because M3 GPUs are still slowed down by multiple user loads. Also, M3 has a maximum run time of 7 days; our server has indefinite run time. 
* Full list of M3 cluster specs [here](http://docs.massive.org.au/M3/m3users.html)

We have 3 major data-serving resources:

1. The /data partition on our room 217 server, with a total of 500 Gb. 
2. Any `/<project>` and `/<project_scratch>` shared folders on M3 - the former is backed up weekly, the latter is not. Check that you have access to these (you should see a symlink on your home directory); otherwise, contact the M3 help desk. See [here](http://docs.massive.org.au/M3/file-systems-on-M3.html) for how M3 advises their folder systems to be used. 
3. The Monash shared drive, or S:drive. See how to access it [here](https://www.monash.edu/esolutions/data-storage/how-to-map-s-drive). This could be used for archival storage, but ultimately, it has the major I/O problem of not being easily command-line accessible. 

## Usage Guidelines

* Use our server for phylogenetics software, and M3 for multithread-heavy software (typically NGS).
* Data is backed up on M3, because they have a dedicated sysadmins, backup schedules and data-serving services. Keep a copy of your data there, in our `/<project>` folder (e.g. `/bm14`). 
* If you need to park a copy of your data in our server, put it in the `/data` if you want to allow global access; otherwise keep it in your home folder (feel free to `chmod` to other users as you please). There is no backup scheduler in place, though, because there's already one on M3. 


## Glossary of Terms

* **Process** - the execution of a computer program[1].  In SLURM/hpc terminology, this is a synonym for *task*. 
* **Thread (of execution)** - the smallest unit of computation that can be managed independently by a scheduler[2]. Another handy way to think about it, from [this reddit ELI5](https://www.reddit.com/r/explainlikeimfive/comments/5xcjnc/eli5_what_exactly_is_the_difference_between_cores/): _"A thread...is a sequence of instructions. A multi-tasking computer has a LOT of threads running at the same time, and so the cores must switch between them, mostly depending upon how much time they need. However, this switch is expensive with regards to time because the state of one thread must be preserved so that when it gets reinstated, it can start up from where it left off. So, all of the register contents need to be saved along with a lot of invisible state variables."_
* **Multithreading** - Threads that can be executed simultaneously, instead of one after the other. See [this Reddit ELI5](https://www.reddit.com/r/learnprogramming/comments/31qzw4/eli5_concurrency_and_multithreading/) for an excellent explanation of multithreading and concurrency. 
* **Hyperthreading** - Intel's proprietary simultaneous multithreading technology on Intel CPUs.
* **Node** - What we think of as a single physical machine/box. A *node* can have multiple *cores* (or *processors*).
* **pthreads (POSIX Threads)** - An *execution model* that executes parrallelism, primarily made for UNIX. 
* **OpenMP* - Used for parrallelism *within* a node. 
* **OpenMPI* - Used for parrallelism *between* nodes. 


## Links and References

* [Wikipedia - Process](https://en.wikipedia.org/wiki/Process_%28computing%29)<br>
* [Wikipedia - Threads](https://en.wikipedia.org/wiki/Thread_%28computing%29)<br>
