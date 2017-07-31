This folder contains a bunch of notes from the BEAST 2017 workshop, held in London, 24 - 29 July. Unfortunately, these only contain the notes for lectures in which I actually understood stuff. 

### Impressions
- BEAST is incredibly mathematical. 
- The primary output of BEAST (and BEAST2) is a probability distribution of trees. I guess that this is a discrete distribution of *n* trees, where each tree has a probability P(Tree<sub>i</sub>), for *i = 1...n*. Different model, prior or initial parameter specifications will ultimately affect P(Tree<sub>i</sub>). 

### Workshop Resources
- [Program](https://taming-the-beast.github.io/workshops/Taming-the-BEAST-in-London/)
- [Slides](https://github.com/Taming-the-BEAST/Taming-the-BEAST-2017-London-Lectures). Unfortunately, these are of limited utility without the speaker present to tell you what's happening. Still, they're not *completely* useless. 

### Moving from BEAST to BEAST2
Install these add-ons in BEAUTi:
- bdsky - BDSKY functionality
- MASCOT
- StarBeast2
- CLASSIC_BEAST - presumably BEAST1 functionality
- SNAPP
- BDSSM
- SCOTTI
- BACTER

These are a bunch of add-ons that were introduced in the workshop, some not very relevant, but get them anyway. To install a package, go to `File` --> `Manage Packages`. Select the package that you wish to install, and click the `Install\Upgrade` button. Restart BEAUTi for the changes to take effect. 

**Command Line Option**: use `addon manager` to do this. To see a list of what you can do with it:

```
cd path/to/BEAST 2.4.7
./addonmanager
```

The syntax to add new packages is:
```
addonmanager -add new_package
```

