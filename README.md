# Introduction

*Don Teng*

*Last update: 16 June 2017*

This first introductory page contains a bunch of essential readings to get the basics first. But before we begin, read this article first: *[What Have You Tried?](http://mattgemmell.com/what-have-you-tried/)*, by Matt Gemmell.

Useful sources: Wikipedia, Reddit Explain Like I'm 5 (ELI5), Khan Academy (for undergraduate-level academic concepts), Stackoverflow (for programming), Youtube. 

The point here is not so much the mere acquisition of facts, but the ability to solve problems independently without needing anyone's help. Most people are nice enough to help you, but consider that a privilege, not an entitlement. No matter your personal goals or career aspirations, sthrive to be able to solve problems that other people can't, because, ultimately, the whole point is to become to best at what you do - it's hard to become the best if you're dependent on others to deliver information to you! (Also, once you do become the best, by definition, you can only keep learning by yourself because there'll be no one else good enough to teach you). Experiencing the frustration of multiple dead-ends, having to make decisions with incomplete (or no) information, or being dropped in the deep end with no backup, is all part of the process. 

## Things to Read up on
### Mathematical Concepts
Recommended youtube channel: [mathematicalmonk](https://www.youtube.com/user/mathematicalmonk).  An in-depth knowledge of these concepts is not essential, unless you're aiming to specialize in that area. An undergraduate understanding of these is sufficient. 
 - Linear regression
 - Markov chains
 - Maximum likelihood (RAXML, IQ-Tree, FastTree - pros and cons. Provide references.)
 - Bayesian statistics (BEAST)

### Phylogenetics Concepts
 - [How to interpret a phylogenetic tree](http://epidemic.bio.ed.ac.uk/how_to_read_a_phylogeny), by Andrew Rambaut. Or [this](https://www.khanacademy.org/science/biology/her/tree-of-life/a/phylogenetic-trees) Khan academy video.
 - [Models of DNA substitution](https://en.wikipedia.org/wiki/Models_of_DNA_evolution), from Wikipedia. 

### Programming
Having a good grasp on how to read, if not write, code is helpful, but not essential (though this is expected to change in future). Of all the items on this list, programming is the easiest to learn; preteens and teenagers learn it all the time in their regular school work.
 - Python, or R to start off. IMO, Python is superior to R in every way except for plotting. The Youtube channel [thenewboston](https://www.youtube.com/watch?v=HBxCHonP6Ro&list=PL6gx4Cwl9DGAcbMi1sH6oAMk4JHw91mC_) is a good place to start.
 - Github
 - Bash terminal, and Linux/Mac OS organization. This is not as easy to pick up by yourself (but it's still not that hard).

## Software We Use
In general, try not to install computational software via ESS. 

 - **XCode and XCode Command Line Tools (for Macs)** - sets up your Mac for development work. 
 - **`homebrew` (Mac OSX package manager)** - [here](https://brew.sh/). You'll need XCode first, and maybe XCode CLT as well. Homebrew installs many kinds of software, including scientific software, into the directories of your Mac automatically so you don't have to organize all your software. For instance, use:

```
brew install my_software
```

To see if the `homebrew` version of your software can be installed this way, use:

```
brew search my_software
```

Many of the computational programs are executables, so using `homebrew` will also save you having to mess with your `$PATH` and all that (if you don't know what that is, all the more reason to use `homebrew` - so you don't have to mess around with all that!)

 - **MAFFT (Multiple sequence alignment)** - executable. Get it via `homebrew`. 
 - **RAxML (tree computation using maximum likelihood)** - This is available on M3, so installing this is optional. Allegedly available via `homebrew`, but I never managed to get the `homebrew`-downloaded version working. In any case, it's so terribly slow that you may prefer to send all RAxML jobs to M3 anyway. In any case, [here's](https://github.com/vjlab/resources/blob/master/software-raxml.md) my RAxML installation and quickstart tutorial, because it's probably the clunkiest software on this list - difficult to install and difficult to use. 
 - **IQ-Tree (tree computation using maximum likelihood)** - executable. Get it via `homebrew`. 
 - **FastTree (tree computation)** - executable. Get it via `homebrew`. 
 - **Tree computation** - FastTree, BEAST package. 
 - **Tree drawing** - FigTree, TempEst, R (ggtree library)
 - **Other** - CDhit (picking unique sequences out of a `fasta` file), PAML (Misc. applications), AliViewer (a free version of Genious, but with much fewer functions), Atom (text file viewer)
 
## For Python users:
 - Use Anaconda for automatic package management. [Conda environments](https://conda.io/docs/using/envs.html) are also great for controlling your packages, and version control between Py36 and Py27. 
 - Useful packages: `pandas`, `numpy`, `Biopython`, `xlrd`, `scipy`, `scikit-bio`
 - [Jupyter](http://jupyter.org/) recommended as an IDE. 
