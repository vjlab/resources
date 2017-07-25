# Intro to infectious disease phylodynamics
 - Oliver Pybus: He made up the word "phylodynamics". "Rapidly evolving pathogens are unique in that their ecological evolutionary dynamics occur on the same timescale, and can therefore potentially interact." e.g. "fixation" is a less meaningful term, because it comes and goes so quickly.
 - Phylodynamics loosely encompasses genetic diversity, epidemic dynamics, and virus phenotypes.
 - Flu has strong selective differences, which drives the preservation and extinction of several lineages.
 - Fun fact: maybe 15 years ago, branch lengths were just genetic distance, not time difference!

## Data
 - Gene sequences are sampled at different points in time and from different location
 - Hence, transmission history can be estimated on a real time scale (e.g. years) and in real space (e.g. countries, cities)
 - Phenotypic trait data may be available as well (e.g. drug resistance)

## Same sampling times, diff rates of evolution
 - Both the x and y axes are time scales! (see picture)
 - "heterochronous" or "serially sampled" (c.f. Measurably-evolving populations), vs. "isochronous" or "contemporaneous sampling".
 - Use TempEst to determine if your sequences are heterochronous - Do they exhibit a correlation between genetic divergence and time? The x intercept is the date of the common ancestor, gradient = rate of evolution, etc. Outliers will lie too far from the line of best fit, i.e. evolved too little or too much given their time stamp.
 - Rapidly evolving pathogens are not the only source of heterochronous data: ancient DNA can be recovered from extremely old biological material (>100k years old)
 - Phylodynamic analysis can still be applied to isochronous data, but statistical power is weaker. External information about rates or dates is probably needed as well.

## Some Phylodynamic Questions
 - (see slide) Questions on the right are more meaningful than questions on the left.
 1. Phylogenetic tree - shows shared ancestry
 2. Molecular clock - places ancestral on a temporal frame of reference
 3. Coalescent/BD models - links ancestry to pop dynamics. We use the rate at which branches coalesce to infer population size. It just works, because maths is like magic. Note: best to remove data points that are epidemiologically linked, e.g. samples from the same family in the same location during that epidemic.
 4. Phylogeography - where did stuff occur? Well, just colour the branches/tips by location, really. Apparently, we can also infer the most likely location of an unknown on the tree.
 5. Selection analysis - dN/dS, etc.
 6. Recombination - Horizontal gene transfer: different parts of the genome would have different trees! It would look like a node/tip has >1 origin. e.g. 5' region and 3' region.  Trying to draw a tree from the whole genome would look like a mess, for obvious reasons.  Screen the data first for a recombination signal (how???). Maybe samples with recombination would switch between membership of major clades, like, 50% of the time.

## Bits
 - Oliver never uses the estimated rate of evolution from TempEst as a prior.
 - Out of nowhere: partial genomes tend to push back the TMRCA further and further into the past, which is a bias that Oliver and Alexei can't quite explain.
 - Oliver: Negatively-sloping gradient in TempEst: means that the sequence data and dates alone are insufficient to infer params like TMRCA. There's no point cutting out large chunks of the dataset as well to get a heterochronous subset either. Gotta use external data to find meaningful priors for this.
 - Oliver: there's a lot of junk published out there; there ought to be a BEAST license to verify that the user knows how to use BEAST, before he's allowed to cite it.
 - Stephane: he didn't directly say this, but an *under-specified model* (i.e. where we didn't pre-define all the params, or priors) that still looks good upon qualitative assessment is still a good model. In fact, it might be superior to a more elaborately specified one, simply because it's simpler (shows that the additional prior/param is, in fact, superflous). 
