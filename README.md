# Introduction

*Don Teng*

This first introductory page contains a bunch of essential readings to get the basics first. But before we begin, read this article first: *[What Have You Tried?](http://mattgemmell.com/what-have-you-tried/)*, by Matt Gemmell.

Useful sources: Wikipedia, Reddit Explain Like I'm 5 (ELI5), Khan Academy (for undergraduate-level academic concepts), Stackoverflow (a Q&A site for programming), Youtube. 

The point here is not so much the mere acquisition of facts, but the ability to solve problems independently without needing anyone's help. Most people are nice enough to help, but, well, it's not nice to keep bugging someone when the exact same content is available on Youtube. These Youtube videos are made by people who make a living out of producing such tutorials and content, so they'll definitely be much better at *teaching* stuff. 

Unfortunately, almost all the software we use is not very well-documented, or the documentation is written in a way that's only accessible to intermediate users. In this case, there's usually a "default setting" that work for most cases - go with that. Otherwise, enter random numbers just to see what errors you get - or if the program returns garbage, this is good information too, because you can then figure out *why* it's garbage.

## About This Repo
This repo contains several tutorial files, with varying levels of difficulty.  There's not much in the way of progression, you should be able to start wherever you want. Some tutorials have recommended prerequisites, these will be listed near the top of that tutorial. 

The resources are loosely classified into themes, reflected in the title. For instance, we have a bunch of tutorials about the high-performance computing facility at Monash (M3), all prefixed with "m3", e.g. `m3-quickstart`, `m3-about-the-hpc`, and so on. 

## Things to Read up on
Realistically, the time frames for finishing all the items to read up on in this section are something like:
 - Theoretical knowledge - two to three months
 - Working knowledge - about half a year
 - Subject matter expert - the rest of your life

### Mathematical Concepts
Recommended youtube channel: [khan academy](https://www.youtube.com/user/khanacademy) for undergrad-level theory, and [mathematicalmonk](https://www.youtube.com/user/mathematicalmonk) for higher-level concepts.  An in-depth knowledge of these concepts is not essential, unless you're aiming to specialize in that area. An undergraduate understanding of these is sufficient. Read up on the Wikipedia articles on the following, and any tutorial videos you can find. 
 - Linear regression
 - Markov chains
 - Maximum likelihood
 - Bayesian statistics
 - MCMC - the most difficult of the lot. Don't bother if you don't need to know this. 
 
The domain-specific application of these to phylogenetics will be covered in tutorials available in this repo (coming soon). 

### Phylogenetics Concepts
 - The Wikipedia article on [computational phylogenetics](https://en.wikipedia.org/wiki/Computational_phylogenetics) is a pretty good starting point. Admittedly, passive reading is a pretty dry and ineffective way to learn; there are "learn by doing"-style tutorials in the works. 
 - [How to interpret a phylogenetic tree](http://epidemic.bio.ed.ac.uk/how_to_read_a_phylogeny), by Andrew Rambaut. Or [this](https://www.khanacademy.org/science/biology/her/tree-of-life/a/phylogenetic-trees) Khan academy video.
 - [Models of DNA substitution](https://en.wikipedia.org/wiki/Models_of_DNA_evolution), from Wikipedia. 
 - [Hierarchical clustering](https://en.wikipedia.org/wiki/Hierarchical_clustering). Otherwise known as "[neighbour joining (NJ)](https://en.wikipedia.org/wiki/Neighbor_joining)" in phylogenetics literature. We don't use NJ trees very often, but it's a good conceptual starting point, and is easy enough to do by hand. 

### Programming
Having a good grasp on how to read, if not write, code is helpful, but not essential (though this is expected to change in future). Of all the items on this list, programming is the easiest to learn - it's a gentle but extremely long learning curve. 
 - Python, or R to start off. IMO, Python is superior to R in every way except for plotting. The Youtube channel [thenewboston](https://www.youtube.com/watch?v=HBxCHonP6Ro&list=PL6gx4Cwl9DGAcbMi1sH6oAMk4JHw91mC_) is a good place to start.
 - Github. There are three ways to learn this: using the website interface that you're looking at right now, using a [Github desktop application](https://desktop.github.com/) (quite useless), and command line. It's best to just learn the command line, because it allows you to do the most things. Here's a [recommended video](https://www.youtube.com/watch?v=HVsySz-h9r4). 
 - Bash terminal, and Linux/Mac OS organization.

## Software We Use
The following is a list of frequently-used-software. In general, try not to install computational software via ESS. Unfortunately, the installation instructions shown here are only for Macs. 

 - **XCode and XCode Command Line Tools (for Macs)** - sets up your Mac for development work. Get these first and foremost, because many of the computational programs require these to install properly. 
 - **`homebrew`** - A Mac OS package manager. Get it [here](https://brew.sh/). You'll need XCode first, and maybe XCode CLT as well. Homebrew installs many kinds of software, including scientific software, into the directories of your Mac automatically so you don't have to organize all your software. For instance, to install software, use:

```
brew install my_software
```

To see if the `homebrew` has your software available:

```
brew search my_software
```

Many of the computational programs are executables, so using `homebrew` will also save you having to mess with your `$PATH` and all that (if you don't know what that is, all the more reason to use `homebrew`!)

 - **MAFFT** - For multiple sequence alignment. An executable. Get it via `homebrew`. 
 - **RAxML** - For computing trees using maximum likelihood. This is available on M3, so installing this is optional. Allegedly available via `homebrew`, but I never managed to get the `homebrew`-downloaded version working. In any case, it's so terribly slow that you may prefer to send all RAxML jobs to M3 anyway. In any case, [here's](https://github.com/vjlab/resources/blob/master/software-raxml.md) my RAxML installation and quickstart tutorial, because it's probably the clunkiest software on this list - difficult to install and difficult to use. 
 - **IQ-Tree** - For tree computation using maximum likelihood. An executable. Get it via `homebrew`. 
 - **FastTree** - Fast tree computation. An executable. Get it via `homebrew`. 
 - **BEAST package** - For tree computation using Bayesian statistics. Also has other secondary uses related to the understanding its own output, because the algorithms used to compute a Bayesian tree are not easy to understand. Version 1.8.4 is available [here](http://beast.bio.ed.ac.uk/); that BEAST package also consists of accessory programs `Tracer` v1.6 and `BEAGLE` v2.1. Note that there's a [version 2](https://www.beast2.org/) available, though we're mostly still using version 1 so far. 
 - **FigTree** - a nice, lightweight program for tree drawing. Simple installation. 
 - **TempEst** - another nice program for tree drawing. We use it over FigTree because of one particular "find best root" function that's not available in `FigTree`. 
 - **CDhit** - For clustering DNA sequences by similarity. An executable; get it via `homebrew`. 
 - **PAML** - Multi-purpose analysis package with miscellaneous uses. 
 - **AliViewer** - Allows you to look at a `.fasta` file of sequence data. 
 
## For Python users:
 - Use Anaconda for automatic package management. [Conda environments](https://conda.io/docs/using/envs.html) are also great for controlling your packages, and version control between Py36 and Py27. 
 - Useful packages: `pandas`, `numpy`, `Biopython`, `xlrd`, `scipy`, `scikit-bio`
 - [Jupyter](http://jupyter.org/) recommended as an IDE. 
