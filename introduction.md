# Introduction
This first introductory page contains a bunch of essential readings to get the basics first. But before we begin, read this article first: *[What Have You Tried?](http://mattgemmell.com/what-have-you-tried/)*, by Matt Gemmell.

Useful sources: Wikipedia, Reddit Explain Like I'm 5 (ELI5), Khan Academy (for undergraduate-level academic concepts), Stackoverflow (for programming), Youtube. 

The point here is not so much the mere acquisition of facts, but the ability to solve problems independently without needing anyone's help. Most people are nice enough to help you, but consider that a privilege, not an entitlement. No matter your personal goals, career aspirations, or stage in life, the whole point is to be able to solve problems that other people can't. Experiencing the frustration of multiple dead-ends, having to make decisions with incomplete (or no) information, or being dropped in the deep end with no backup, is all part of the process. 

## Things to Read up on
### Mathematical Concepts
Recommended youtube channel: [mathematicalmonk](https://www.youtube.com/user/mathematicalmonk).  An in-depth knowledge of these concepts is not essential, unless you're aiming to specialize in that area.
 - Linear regression
 - Markov chains
 - Maximum likelihood (RAXML, IQ-Tree, FastTree - pros and cons. Provide references.)
 - Bayesian statistics (BEAST)

### Phylogenetics Concepts
 - [How to interpret a phylogenetic tree](http://epidemic.bio.ed.ac.uk/how_to_read_a_phylogeny), by Andrew Rambaut. Or [this](https://www.khanacademy.org/science/biology/her/tree-of-life/a/phylogenetic-trees) Khan academy video.
 - [Models of DNA substitution](https://en.wikipedia.org/wiki/Models_of_DNA_evolution), from Wikipedia. 

### Programming
Having a good grasp on how to read, if not write, code is helpful, but not essential (though this is expected to change in future). The Youtube channel [thenewboston](https://www.youtube.com/watch?v=HBxCHonP6Ro&list=PL6gx4Cwl9DGAcbMi1sH6oAMk4JHw91mC_) is a good place to start.
 - Python, or R to start off. IMO, Python is superior to R in every way except for plotting. 
 - Github

### Writing & Communication
This is starting to become a sticking point in science, not just in terms of a scientist speaking to a non-specialist audience, but [specialists speaking to other specialists from other fields](http://blogs.agu.org/sciencecommunication/2010/10/26/dude-you-are-speaking-romulan/). 
- An [excellent article](http://phenomena.nationalgeographic.com/2010/11/24/on-jargon-and-why-it-matters-in-science-writing/) on excessive use of jargon in biology.
 - [Convoluted jargon](http://www.cbronline.com/news/cloud/aas/mystifying-it-jargon-creates-costly-uk-business-ignorance-4655127/) is expensive - there is a very real material cost of confusion and miscommunication.
 - [Excessive jargon](https://www.fastcompany.com/3052242/the-secret-to-sounding-smart-using-simple-language) (are you sensing a theme here?) makes the author sound stupid anyway.

My personal take:
 - Avoid jargon, or even big words, because this is not grade school and you don't have a teacher to give you a gold star for showing off your vocabulary. On the contrary, you're more likely, as a reader, to be impressed by a writer who can explain complex ideas in simple terms. Don't try to sound smart, just be smart.
 - Don't write like a scientist: stop using that writing style in publications which I think of as "academic deadpan". 
 - [Avoid passive voice](https://www.reddit.com/r/AskScienceDiscussion/comments/1aq96g/why_is_scientific_writing_mainly_in_the_passive/), e.g. say *"I baked a cake"* instead of *"The cake was baked"* or *"The cake was baked by me"* - both of which sound super weird anyway! A common defence of using passive voice is that it "sounds objective". Don't try to sound objective, just be objective.

Stop using these words forever:
 - *utilize* - *"use"* is fine. 
 - *novel* - of course it's novel, otherwise you wouldn't be writing about it. 
 - *morphology* - *"structure"*, *"form"*, *"shape"* are all fine. 
 - *enrich* - if you're a bioinformatician. Many bioinformatics papers use this as a catch-all verb when they can't think of a better word. 

See [this](https://github.com/jtleek/datasharing) guideline on how to share data with a statistician.

## Software We Use
In general, most of these are available using `homebrew`. Do a `brew search` first to see if it's available, because `brew` manages all your packages and directories automatically.
 - **Multiple Sequence Alignment** - MAFFT.
 - **Tree computation** - RAxML, IQ-Tree, FastTree, BEAST package. 
 - **Tree drawing** - FigTree, TempEst, R (ggtree library)
 - **Other** - CDhit (picking unique sequences out of a `fasta` file), PAML (Misc. applications), AliViewer (a free version of Genious, but with much fewer functions), Atom (text file viewer)
 
For Python users:
 - Use Anaconda for automatic package management, and `conda install <package>` for library management.
 - Useful packages: `pandas`, `numpy`, `Biopython`, `xlrd`
 - [Jupyter](http://jupyter.org/) recommended for an IDE. 
