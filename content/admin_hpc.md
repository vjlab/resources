# R Setup
A bunch of admin notes for HPC admin.

## Admin tools

* `quota` and `quotatools`: Obtained via `apt-get`. Not set up yet, only downloaded. **Danger**: may involve editing `/etc/fstab` which is easily damaged, and may render the system un-bootable! **PROCEED WITH EXTREME CAUTION.** See a rough walkthrough [here](http://computingtech.blogspot.com.au/2008/09/ubuntu-linux-disk-quotas.html)
* `sysinfo`. Access using `$ sysinfo`.
* Nice askubuntu [post](https://askubuntu.com/questions/503216/how-can-i-set-a-single-bashrc-file-for-several-users/503222) about copying global bashrc's for everyone.

## Usual admin commands

 - After adding a new user, add him to the `Allowed Users` in `/etc/ssh/sshd_config`. Restart the ssh service with `service sshd restart`

## User `bashrc` management
(not working)
[src](https://askubuntu.com/questions/503216/how-can-i-set-a-single-bashrc-file-for-several-users/503222)

 - Create a backup: `sudo cp /etc/bash.bashrc /etc/bash.bashrc-backup`

## Phylogenetics Software

_IMPT note: apps are slowly being migrated to a single shared folder, `/home/dten0001/apps`. I'm choosing a single custom `apps` folder for complete control over installation and updating, though these need not live in my personal home folder. I might move this elsewhere furthur up the FHS when I find a more suitable location._

Simply `ls` the shared `apps` folder to see what's in there!

* BEAGLE: I frankly have no idea. It's not in `/user/local/`. 
* Figtree: Installed via `apt-get`
* fasttree: Installed via `apt-get`

## Other
* dspp: Installed via `apt-get`
* bowtie, bowtie2: Installed via `apt-get`
* samtools: Installed via SF download and `make install`. It's automatically placed in `/user/local/bin`, I think.
* SPAde: Local install, no path. So far, only used for `Unicycler`; use `--spade_path path/to/spade` to specify path.

## Installing Docker

[src](https://gist.github.com/Simplesmente/a84343b1f71a46bbeedbb6c9b20fa9c1)

```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates -y
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo echo 'deb https://ubuntu.cozycloud.cc/debian trusty main' | sudo tee /etc/apt/sources.list.d/cozy.list > /dev/null
sudo apt-get update
sudo apt-get purge lxc-docker
sudo apt-get install linux-image-extra-$(uname -r) -y
sudo apt-get install docker-engine cgroup-lite apparmor -y
sudo usermod -a -G docker $USER
sudo service docker start
```


## R: Installing shared libraries
Not sure if how to organize it such that users can install their own insulated packages if required (or maybe I'll just install packages on request to prevent compatibility debt from building up). Anyway, from within the R environment, use `.libPaths()` to see which paths are accessible to the R executable.
"/>

Global libraries are much better setup (compared to Python). Global libraries should be installed in `/usr/lib/R/site-libraries`. [source](https://stat.ethz.ch/pipermail/r-help/2003-October/041178.html). Use `sudo R` to start up R with admin privileges, and run:

```
install.packages("my_package", lib="/usr/lib/R/site-libraries")
``` 

Check out this University cluster webpage for how they did their setup: https://www.chpc.utah.ed
u/documentation/software/r-language.php.

Note that `adephylo` refuses to be installed, for some strange reason. 

# Python Setup

**IMPT: do NOT use `sudo pip install my_package`!** [Reason.](https://askubuntu.com/questions/802544/is-sudo-pip-install-still-a-broken-practice)

Check out Andrew Perry's `miniconda` [set up tutorial/recipe](https://github.com/MonashBioinformaticsPlatform/bioconda-tutorial/blob/master/Bioconda_Installation.ipynb).

**pro-tip**: use `which <program>` to find out which version (global or `miniconda` installed) is being called, if you've got more than 1 version living somewhere on the machine. e.g.: 

```
$ which beast-mcmc
/usr/bin/beast-mcmc
$ which beast
/home/dten0001/Downloads/beast2/bin/beast
```

Frankly, I didn't initially track whether libraries should be globally installed (because I didn't think to do so), so much of what's on there now is quite messy; lost track of what site-packages are on the PATH. Users are recommended to `conda install` whatever they need to their local conda `env`. There's a global install of Anaconda in `/opt/anaconda`, but this can't be conda-updated easily, so the current workaround is just containerise *everything*, with no global libraries, for each user. I have my own local installation in `~/anaconda3`, which `sys.path` knows about, so I'll likely remove the `/opt/anaconda` global install if it's not being used.

**Try this**: Install a multi-user env in a global location. https://conda.io/docs/user-guide/configuration/admin-multi-user-install.html

Containerization done using `conda`. See [this page](https://conda.io/docs/commands.html#conda-vs-pip-vs-virtualenv-commands) for conda vs. pip vs. virtualenv info. Some exploration commands:

* `conda info --envs` - to see what environments have been set up
* `conda list` - from an activated environment, to see what packages have been conda or pip-installed
* `pip list` - to see what packages have been pip-installed. 
* `pip show <my_package>` - to see where `my_package` was pip-installed. This should ideally be a global location.

Shared Anaconda installation: installed in `/opt/anaconda3`. See [this](https://stackoverflow.com/questions/27263620/how-to-install-anaconda-python-for-all-users) SO post.

References:

* Read up about [conda: myths and misconceptions](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/)
