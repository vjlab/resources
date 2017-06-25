# File Formats and Naming Conventions
## Virus Name Conventions
Virus names are often (but unfortunately not always) named like:

```
<virus>/<sample location>/<any other information>/<collection date>
```

Some examples of influenza B virus names:

```
B/Arizona/02/2002-05-04
B/Arizona/02/2002-05
B/Arizona/02/2002
```

The hassle of cleaning names is probably the most tedious, but necessary, chore. Watch out for all these: 
 - Duplicate name + Ids - could have resulted from multiple submissions of the same sequence to the same data source, maybe by different labs. 
 - Duplicate names - the same sample could have been given to different labs, then sequenced separately. 
 - special characters (for RAxML) and white spaces (for FigTree). Look out especially for semicolons and brackets, because these will mess up the newick format of trees. 
 - nucleotide characters other than 'a', 'c', 'g', 't' (CDHit)
 - Duplicate sequences (MAFFT)
 
## Frequently-used File Formats
### Sequence Data
**`.fasta`** - probably the most important file format. Example:

```
>Turkey
AAGCTNGGGCATTTCAGGGTGAGCCCGGGCAATACAGG
>Salmo gair
AAGCCTTGGCAGTGCAGGGTGAGCCGTGGCCGGGCACGGTATAGCCGT
>H. Sapiens
ACCGGTTGGCCGTTCAGGGTACAGGTTGGCCGTTCAGGGTAA
>Chimp
AAACCCTTGCCGTTACGCTTAAACCGAGGCCGGGACACTCAT
>Gorilla
AAACCCTTGCCGGTACGCTTAAACCATTGCCGGTAC
```

The bit after the arrow ">" is the header. This is what defines a `.fasta` format.

**`.phy`** - phylip format. An example:
  
```
        5    42
Turkey    AAGCTNGGGC ATTTCAGGGT GAGCCCGGGC AATACAGGGT AT
Salmo gairAAGCCTTGGC AGTGCAGGGT GAGCCGTGGC CGGGCACGGT AT
H. SapiensACCGGTTGGC CGTTCAGGGT ACAGGTTGGC CGTTCAGGGT AA
Chimp     AAACCCTTGC CGTTACGCTT AAACCGAGGC CGGGACACTC AT
Gorilla   AAACCCTTGC CGGTACGCTT AAACCATTGC CGGTACGCTT AA
```
- The numbers "5" and "42" are the number of sequences and the lengths of the sequences themselves, respectively.
- All sequences must be of the same length.
- The sequence names must have the same length, padded by white spaces as necessary. Longer sequence names will be truncated, which is supremely annoying. 
- `.phy` is probably the most annoying file format to deal with. Fortunately, I've never had to use it before because any program which accepts `.phy` can also accept `.fasta` formats, so I'm hoping that this will die a natural death. 

### Tree file extensions - `.tre`, `.nex`, `.nwk`
### BEAST input - `.xml`
Fortunately, generating this file can be done so quite easily in `BEAUTi`, so there's no need to go into great detail. However, you may sometimes wish to make minor tweaks to an existing `.xml` directly instead of doing the whole shebang with `BEAUTi` all over again. The main sections to look out for are:
 - Chain length - That is, MCMC chain length. Ctrl-F "chainLength". This is normally set to 200M to 500M. 
 - Interval length - the number of states between which we'll discard, typically set to 20,000. That is: we only record 1 state every 20,000 states (technical reason: to avoid autocorrelation between samples). 
 - File name - The names of output files that `BEAST` returns. Ctrl-F "filename"; this should occur three times.
