## Software We Use

The following is a list of frequently-used-software. In general, try not to install computational software via ESS. The installation instructions shown here are only for Macs.

### Generic Software

 - **XCode and XCode Command Line Tools (for Macs)** - sets up your Mac for development work. Get these first and foremost, because many of the computational programs require these to install properly.
 - **`homebrew`** - A Mac OS package manager. Get it [here](https://brew.sh/). You'll need XCode first, and maybe XCode CLT as well. Homebrew installs many kinds of software, including scientific software, into the directories of your Mac automatically so you don't have to organize all your software. For instance, to install software, use:

```
brew install my_software
```

To see if `homebrew` has your software available:

```
brew search my_software
```

Many of the computational programs are executables, so using `homebrew` will also save you having to mess with your `$PATH` and all that (if you don't know what that is, all the more reason to use `homebrew`!)

 - Python3
 - R (from R Studio)
 - `blastn`, `blastx` (CLI preferred)

### Phylogenetics Software

 - **MAFFT** - For multiple sequence alignment. An executable. Get it via `homebrew`.
 - **RAxML** - For computing trees using maximum likelihood. This is available on M3, so installing this is optional. [Here's](https://github.com/vjlab/resources/blob/master/software-raxml.md) my RAxML installation and quickstart tutorial.
 - **IQ-Tree** - For tree computation using maximum likelihood. An executable. Get it via `homebrew/science`.
 - **FastTree** - Fast tree computation. An executable. Get it via `homebrew/science`.
 - **BEAST v1.8.4, v2.x** - For tree computation using Bayesian statistics. Has a few other programs for post-processing BEAST output.
 - **FigTree** - a nice, lightweight program for tree drawing. 
 - **TempEst** - another nice program for tree drawing. 
 - **CDhit** - For clustering DNA sequences by similarity. 
 - **PAML** - Multi-purpose analysis package with miscellaneous uses.
 - **Treesub** - For plotting amino acid changes along a tree. Java-compiled. Get it [here](https://github.com/tamuri/treesub)
 - **HyPhy CLI/GUI** - for selection analysis
 - **Datamonkey** - Web app, so no installation required. _Hidden constraint that they don't announce beforehand: Can only accept a max of 500 sequences._
 - **Antigenic cartography** - Web app.
 - **AliViewer** - Allows you to look at a `.fasta` file of sequence data.

## For Python/R programmers:
 - conda for automatic package management. [Conda environments](https://conda.io/docs/using/envs.html) are also great for controlling your packages, and version control between Py36 and Py27.
 - Useful packages: `anaconda`, `pandas`, `numpy`, `Biopython`, `xlrd`, `scipy`, `scikit-bio`
 - `pip`
 - [Jupyter](http://jupyter.org/) recommended as an IDE.
 - atom
 
 ## Things to Read up on
-----

### Mathematical Concepts
Recommended youtube channel: [khan academy](https://www.youtube.com/user/khanacademy) for undergrad-level theory, and [mathematicalmonk](https://www.youtube.com/user/mathematicalmonk) for higher-level concepts.  An in-depth knowledge of these concepts is not essential, unless you're aiming to specialize in that area - you certainly don't need to know how to do the maths by hand. An undergraduate understanding of these is sufficient; even Wikipedia is a little overkill.

 - Linear regression
 - Markov chains
 - Maximum likelihood
 - Bayesian statistics
 - MCMC - the most difficult of the lot. Don't bother if you don't need to know this.

### Phylogenetics Concepts
 - The Wikipedia article on [computational phylogenetics](https://en.wikipedia.org/wiki/Computational_phylogenetics) is a good starting point - it's sufficiently comprehensive that, at least, you'll be able to pinpoint what you don't know and look for that elsewhere. Also, admittedly, passive reading is a pretty dry and ineffective way to learn; there are "learn by doing"-style tutorials in the works.
 - [How to interpret a phylogenetic tree](http://epidemic.bio.ed.ac.uk/how_to_read_a_phylogeny), by Andrew Rambaut. Or [this](https://www.khanacademy.org/science/biology/her/tree-of-life/a/phylogenetic-trees) Khan academy video.
 - [Models of DNA substitution](https://en.wikipedia.org/wiki/Models_of_DNA_evolution), from Wikipedia.
 - [Hierarchical clustering](https://en.wikipedia.org/wiki/Hierarchical_clustering). Otherwise known as "[neighbour joining (NJ)](https://en.wikipedia.org/wiki/Neighbor_joining)" in phylogenetics literature. We don't use NJ trees very often, but it's a good conceptual starting point, and is easy enough to do by hand.

### Programming
Having a good grasp on how to read, if not write, code is helpful, but not essential.

 - Python, or R to start off. IMO, Python is superior to R in every way except for plotting. The Youtube channel [thenewboston](https://www.youtube.com/watch?v=HBxCHonP6Ro&list=PL6gx4Cwl9DGAcbMi1sH6oAMk4JHw91mC_) is a good place to start.
 - Github. Here's a [recommended video](https://www.youtube.com/watch?v=HVsySz-h9r4).
 - Bash terminal, and Linux/Mac OS organization.
