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
 - Duplicate name + Ids
 - Duplicate names
 - special characters (for RAxML) and white spaces (for FigTree)
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
- `.phy` is probably the most annoying file format to deal with. Fortunately, I've never had to use it before because any program which accepts `.phy` can also accept `.fasta` formats. I'm hoping that this format will die a natural death. 

 ### Tree file extensions - `.tre`, `.nex`, `.nwk`
 ### BEAST input - `.xml`
