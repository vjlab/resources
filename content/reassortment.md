# Thoughts On Reassortment

The few reassortment analyses I've done so far were performed with the Mk1 Eyeball, i.e. looking at the 8 trees of full genomes, and seeing if the same names appear in the same clades.  All this is predicated on the assumption that *if there is no reassortment, phylogenies for all internal genes will have the same shape*. Is this necessarily true?

**TLDR: I don't believe so.** 

In order for that assumption to hold true, the different lineages/clades must have had enough time to establish themselves as genotypically distinct entities to other lineages/clades, having evolved according to whatever idiosyncratic selective pressures they face. Some necessary conditions might be: low transmissibility, such that we get reasonably good geographic or temporal clustering, and a sufficiently-high mutation rate that "outpaces" transmission rates. The ultimate nightmare scenario for this is Flu B. The global tanglegram has no meaningful geographic or temporal clustering (and yet Flu B still hangs around, and the two lineages continue to co-circulate). It may be easier to disentangle H3N2 reassortment, but for strong environmental forces that nearly wipe out circulating seasonal A/H3N2 almost yearly, such that even reassortment confers no selective advantage against environmental forces. 

## An Example
Let's compare two imaginary flu-like viruses, spreading in, say, the United States: 

* virus X, with a mutation rate on the order of 10E-3, which requires blood, saliva, or mucus contact to transmit to another host.  
* virus Y, which all the exact same attributes, except that all susceptible hosts within 10m of an infected person will get infected as well. 

Obviously, virus Y is much, much more transmissible than virus X.  The phylogeny of virus Y would show almost no geographic clustering at all, because the virus rapidly gets transmitted everywhere.  The phylogeny of virus X, however, would demonstrate a much clearer geographic clustering, and due to the slower mechanism of transmission, would exhibit a stronger temporal signal. 

(In any case, the resultant phylogenies would be an interesting [chaotic](https://en.wikipedia.org/wiki/Chaos_theory) interplay between immunological, environmental and epidemiological forces that may actually lend themselves well to predictive DE modelling, if not descriptive statistics.)

## Simulation Study

* Init a set of full-genome sequences, allowed to mutate at 10E-3 substitutions per site per year. We can grant a higher probability of mutation to known informative sites. We can also model each virus to have a fixed lifetime, e.g. 5 years, though realistically viruses aren't supposed to die of old age. 
* Allow viruses to reproduce: Every week, each virus will produce another x copies of themselves. 
* Add reassortment into the reproduction mechanism: whenever a child virus is created, it has a chance to randomly select another nearby child virus, and randomly swap some segments with it. 
* Init, say, 3 equidistant regions (analogous to geographic locations) that the viruses can "spread" to, at region-specific import/export rates. 
* Each region can have an ongoing selection pressure: randomly select 1 (or a few?) sequences, and kill off any virus that's not at least 90% similar to the selected sequences. 
* Every fixed time period, introduce an "environmental selection force" which selects a 1 or more random sequences, then kills off all viruses at all sites that are not at least 90% similar to the selected sequences. This is to simulate seasonal flu. 

If we tweak all the parameter values in this simulation, what would the resulting phylogenies look like?  Can we play with this simulation until we can emulate real-world phylogenies? If two child viruses reassorted, resulting in a significantly genetically-different offspring, would this necessarily result in higher survivability? Or maybe even among the reassortants, those that are *too* genetically divergent would end up dying off as well; there's no reason why merely being genetically different would confer an advantage.
