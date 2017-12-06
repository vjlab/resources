# Introduction
-----

*Don Teng*

This first introductory page contains a bunch of essential readings to get the basics first. Useful sources: Wikipedia, Reddit Explain Like I'm 5 (ELI5), Khan Academy (for undergraduate-level academic concepts), Stackoverflow (a Q&A site for programming), Youtube.

## Contents
This repo contains several tutorial files, with varying levels of difficulty.  Recommended prerequisites will be listed near the top of that tutorial. However, try as I might to make them so, there's no guarantee that each tutorial is entirely self-contained, but the idea is that you should be able to start anywhere.

1. #### Phylogenetics
 - [`Commonly used file formats`](./content/misc-file-formats.md) - Tutorial on commonly used file formats like `fasta`, `phy`, etc.
 - [`Multiple sequence alignment - introduction`](./content/alignment1-introduction.md) - How to do multiple sequence alignment, part 1
 - [`Multiple sequence alignment using MAFFT`](./content/alignment2-mafft.md) - How to do multiple sequence alignment (using `mafft`), part 2
 - [`Software for tree reconstruction`](./content/methods-tree-computation.md) - How to use various programs to compute a tree, and their pros and cons
 - [`BEAST tutorial links`](./content/software-beast.md) - A link to existing BEAST tutorials.
 - [`PAML-TREESUB`](./content/software-paml-treesub.md) - How to install and use `PAML`, and an associated program, `treesub`.
 - [`RAxML`](./content/software-raxml.md) - How to install RAXML, and basic usage.

2. #### Using high-performance computers
 - [`about-our-hpc`](./content/about-our-hpc.md) - How to use the lab's internal server, located in room 217
 - [`m3-about-the-hpc`](./content/m3-about-the-hpc.md) - WIP. Some resources, glossary of terms.
 - [`m3-quickstart`](./content/m3-quickstart.md) - A tutorial on how to send a job to M3.
 - [`m3-tips-and-tricks`](./content/m3-tips-and-tricks.md) - A dumping ground for how to use M3 slightly more efficiently.

3. #### Other miscellaneous
 - [`data-wrangling`] - *Upcoming*. Some recommended practices for virus name configurations, what kind of files to prepare, and how to pass data to your RA.
 - [`R-ggtree-demo`](./content/R-ggtree_demo.pdf) - How to plot some basic trees with `ggtree`, in R. This PDF document should be viewable in your browser, but doesn't always; you can download it to view it if required.
 - [`misc-learning-to-code`](./content/misc-learning-to-code.md) - tutorial on how to *learn* to code, not actually on how to code. Has links for the latter.
 - [`software-python-resources`](./content/software-python-resources.md) - A bunch of python resources.
 - [`software-tips-and-tricks`](./content/software-tips-and-tricks.md) - A dumping ground for miscellaneous bash or computational tips and tricks.
 - [`tech-github`](./content/tech-github.md) - Tutorial for basic command line usage of Github.
 - [`misc-writing`](./content/misc-writing.md) - How to write so that others can understand you.
 - [`things-to-read-up-on`](./content/things.md) - Don's things to read up on.
 - [`London BEAST workshop notes`](./beast/readme.md) - Don's notes from London.

4. ### Bioinformatics Projects
 - A principled way to subsample across location and time. Downsampling & representative sampling (these are different situations!). Do BEAST and ML runs to check that tree topologies are preserved in terms of major clade structures (more accurate way to do this with Robinson-Faulds?). My first guess: CD-hit by country/year.
 - Clade membership, the computational way.  Can either use a list of references (vaccines), or unsupervised (K-means). Requires pairwise optimization.
 - The epistasis problem (where's that blog post again?)
 - Reassortment! A principled way to measure it, detect it...
 - Cleaned, aligned databases of all kinds of viruses? Start with all flu viruses. Needs to have a proper way to either automatically update, or easily manual update every week or so. 
 - Dating an ML tree. This is a methodological nightmare, though.
