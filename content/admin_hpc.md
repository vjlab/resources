
# R Setup
A bunch of admin notes for HPC admin.

## Installing shared libraries
Not sure if how to organize it such that users can install their own insulated packages if required (or maybe I'll just install packages on request to prevent compatibility debt from building up). Anyway, from within the R environment, use `.libPaths()` to see which paths are accessible to the R executable.

Global libraries are much better setup (compared to Python). Global libraries should be installed in `/usr/lib/R/site-libraries`. [source](https://stat.ethz.ch/pipermail/r-help/2003-October/041178.html). Use `sudo R` to start up R with admin privileges, and run:

```
install.packages("my_package", lib="/usr/lib/R/site-libraries")
``` 

Check out this University cluster webpage for how they did their setup: https://www.chpc.utah.ed
u/documentation/software/r-language.php.

Note that `adephylo` refuses to be installed, for some strange reason. 

# Python Setup

**IMPT: do NOT use `sudo pip install my_package`!** [Reason.](https://askubuntu.com/questions/802544/is-sudo-pip-install-still-a-broken-practice)

Frankly, I didn't initially track whether libraries should be globally installed, so much of what's on there now is a mess; lost track of what site-packages are on the PATH, and I think that Anaconda is in `/opt/anaconda`, but can't be sure. Users are recommended to `conda install` whatever they need to their local conda `env`. 

Containerization done using `conda`. See [this page](https://conda.io/docs/commands.html#conda-vs-pip-vs-virtualenv-commands) for conda vs. pip vs. virtualenv info. Some exploration commands:

* `conda info --envs` - to see what environments have been set up
* `conda list` - from an activated environment, to see what packages have been conda or pip-installed
* `pip list` - to see what packages have been pip-installed. 
* `pip show <my_package>` - to see where `my_package` was pip-installed. This should ideally be a global location.

Shared Anaconda installation: installed in `/opt/anaconda3`. See [this](https://stackoverflow.com/questions/27263620/how-to-install-anaconda-python-for-all-users) SO post.

References:

* Read up about [conda: myths and misconceptions](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/)
