# About the HPC

## Glossary of Terms
- **Process** - the execution of a computer program[1].  In SLURM/hpc terminology, this is a synonym for *task*. 
- **Thread (of execution)** - the smallest unit of computation that can be managed independently by a scheduler[2]. 
- **Multithreading** - Threads that can be executed simultaneously, instead of one after the other. See [this Reddit ELI5](https://www.reddit.com/r/learnprogramming/comments/31qzw4/eli5_concurrency_and_multithreading/) for an excellent explanation of multithreading and concurrency. 
- **Hyperthreading** - Intel's proprietary simultaneous multithreading technology on Intel CPUs.
- **Node** - What we think of as a single physical machine. A *node* can have multiple *cores* (or *processors*).
- **pthreads (POSIX Threads)** - An *execution model* that executes parrallelism, primarily made for UNIX. 
- **OpenMP* - Used for parrallelism *within* a node. 
- **OpenMPI* - Used for parrallelism *between* nodes. 



Open MPI, SSE
How to run MPI applications (srun)


## Links and References
- 
- [Wikipedia - Process](https://en.wikipedia.org/wiki/Process_%28computing%29)<br>
- [Wikipedia - Threads](https://en.wikipedia.org/wiki/Thread_%28computing%29)<br>
