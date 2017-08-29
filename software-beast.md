# BEAST Tutorial
This is somewhat a cheat - I'm not actually writing the tutorial, but dropping a link to an [already excellent tutorial](https://github.com/trvrb/dynamics-practical) written by Trevor Bedford.  That tutorial gives a demo of a whole analysis pipeline from `BEAUTI` through to `Tracer`, `Figtree` and `TreeAnnotator`.  Ultimately, though, the more difficult question is about the most appropriate choice of parameters to select for the given study. 

This set of [Taming-the-Beast(2)](https://taming-the-beast.github.io/) tutorials are also useful, though applicable only to BEAST 2. 

### Known Issues

 - BEAUTI 2.2 is known to crash whenever you use `Import Alignment` to open a dataset. Last I checked, this mysterious crashing behaviour persisted when I tried to use v2.4.7. Instead of double-clicking on the executable provided, launch from the `/bin` folder instead:

```
cd /Applications/BEAST/ v2.4.7/bin
beauti
```


### Pet Peeve
If I read the documentation correctly, BEAST provides some statistical support for the quality of the tree by recomputing the tree over and over again from the same input - they tend to call this "bootstrap support".  This is *not* called bootstrap, it's called Monte Carlo. [Bootstrap](https://en.wikipedia.org/wiki/Bootstrapping_%28statistics%29) in statistics strictly refers to *sampling with replacement*. A Monte Carlo simulation is a procedure where, say, you wish to find out the probability of heads on a weighted coin (so not necessarily 0.5). Flip the coin 1000 times; the proportion of the number of times that the coin comes up heads will be the empirical probability of heads. That's a Monte Carlo simulation. 
