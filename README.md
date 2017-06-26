# Introduction

*Don Teng*

*Last update: 16 June 2017*

This first introductory page contains a bunch of essential readings to get the basics first. But before we begin, read this article first: *[What Have You Tried?](http://mattgemmell.com/what-have-you-tried/)*, by Matt Gemmell.

Useful sources: Wikipedia, Reddit Explain Like I'm 5 (ELI5), Khan Academy (for undergraduate-level academic concepts), Stackoverflow (for programming), Youtube. 

The point here is not so much the mere acquisition of facts, but the ability to solve problems independently without needing anyone's help. Most people are nice enough to help you, but consider that a privilege, not an entitlement. No matter your personal goals or career aspirations, sthrive to be able to solve problems that other people can't, because, ultimately, the whole point is to become to best at what you do - it's hard to become the best if you're dependent on others to deliver information to you! Experiencing the frustration of multiple dead-ends, having to make decisions with incomplete (or no) information, or being dropped in the deep end with no backup, is all part of the process. 

## Things to Read up on
### Mathematical Concepts
Recommended youtube channel: [mathematicalmonk](https://www.youtube.com/user/mathematicalmonk).  An in-depth knowledge of these concepts is not essential, unless you're aiming to specialize in that area. An undergraduate understanding of these is sufficient. 
 - Linear regression
 - Markov chains
 - Maximum likelihood
 - Bayesian statistics

### Phylogenetics Concepts
 - The Wikipedia article on [computational phylogenetics](https://en.wikipedia.org/wiki/Computational_phylogenetics) is a pretty good starting point.
 - [How to interpret a phylogenetic tree](http://epidemic.bio.ed.ac.uk/how_to_read_a_phylogeny), by Andrew Rambaut. Or [this](https://www.khanacademy.org/science/biology/her/tree-of-life/a/phylogenetic-trees) Khan academy video.
 - [Models of DNA substitution](https://en.wikipedia.org/wiki/Models_of_DNA_evolution), from Wikipedia. 
 - [Hierarchical clustering](https://en.wikipedia.org/wiki/Hierarchical_clustering). Otherwise known as "[neighbour joining (NJ)](https://en.wikipedia.org/wiki/Neighbor_joining)" in phylogenetics literature. We don't use NJ trees very often, but it's a good conceptual starting point, and is easy enough to do by hand. 

### Programming
Having a good grasp on how to read, if not write, code is helpful, but not essential (though this is expected to change in future). 
 - Python, or R to start off. IMO, Python is superior to R in every way except for plotting. The Youtube channel [thenewboston](https://www.youtube.com/watch?v=HBxCHonP6Ro&list=PL6gx4Cwl9DGAcbMi1sH6oAMk4JHw91mC_) is a good place to start.
 - Github
 - Bash terminal, and Linux/Mac OS organization. This is not as easy to pick up by yourself (but it's still not that hard).

Of all the items on this list, programming is the easiest to learn; preteens and teenagers learn it all the time in their regular school work. But programming is not a static set of skills which you learn once and then rely on for the rest of your life: today's cutting-edge technology will become pedestrian in about five years or less. 

## Software We Use
The following is a list of frequently-used-software. In general, try not to install computational software via ESS. Unfortunately, the installation instructions shown here are only for Macs. 

 - **XCode and XCode Command Line Tools (for Macs)** - sets up your Mac for development work. Get these first and foremost, because many of the computational programs require these to install properly. 
 - **`homebrew`** - A Mac OS package manager. Get it [here](https://brew.sh/). You'll need XCode first, and maybe XCode CLT as well. Homebrew installs many kinds of software, including scientific software, into the directories of your Mac automatically so you don't have to organize all your software. For instance, use:

```
   brew install my_software
```

   To see if the `homebrew` has your software available:

```
   brew search my_software
```

   Many of the computational programs are executables, so using `homebrew` will also save you having to mess with your `$PATH` and all that (if you don't know what that is, all the more reason to use `homebrew` - so you don't have to mess around with all that!)

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
