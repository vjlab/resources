# PAML & Treesub

*Written by: Don Teng<br>
Last update: 15 June 2017<br>*

## [PAML](http://abacus.gene.ucl.ac.uk/software/paml.html)
...stands for *Phylogenetic Analysis by ML*. It has several uses, such as inferring ancestral sequences based on modern sequences. 

### Installation
This is actually quite easy, but you're encouraged to get 2 versions:
1. The point-and-click interface
2. The executable file, which `treesub` requires.

## Run
...

## [Treesub](https://github.com/tamuri/treesub)
This is an extension which uses some `PAML` functions, stitched together with RAXML and FigTree. It's primarily useful for producing a tree which shows the amino acid substitutions along the branches. 

### Installation

The repo hasn't been updated in a while, so the installation instructions are slightly out of date. Unfortunately, the bits which are out of date are precisely those bits which are the hardest to install. 

You'll need to get:
1. RAxML (Not easy. See the *RAXML installation tutorial*)
2. PAML executable
3. The latest Java SDK version, which is currently 8. Get it [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
4. FigTree (easy)
5. The [Eclipse](https://www.eclipse.org/downloads/?) IDE, which is not actually used by `treesub`; you need it to get a `treesub.jar` application.

...

### Run
Double-click on the `treesub.jar` file to launch it, like you would a normal application. 

