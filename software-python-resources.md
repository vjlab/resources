# Python Resources
### Get Your Machine Python Ready
[Source](http://www.pyladies.com/blog/Get-Your-Mac-Ready-for-Python-Programming/)
1. Install Xcode

2. Install `homebrew`: 
```
 $ ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

3. Install Python 3. I don't normally bother with Python 2.
```
$ brew install python3
```

4. Install pip.
```
$ curl -O http://python-distribute.org/distribute_setup.py
$ python distribute_setup.py
$ curl -O https://raw.github.com/pypa/pip/master/contrib/get-pip.py
$ python get-pip.py
```

5. Download and install [Anaconda](https://docs.continuum.io/anaconda/install-macos.html#macos-command-line-install), if only just for the conda environment manager.

6. Make a Github account, and install git:
```
brew install git
```

7. Set a PYTHONPATH.

### Really Useful Links
 - [Anatomy of matplotlib](https://github.com/WeatherGod/AnatomyOfMatplotlib) - a comprehensive Matplotlib tutorial.
 - [Python PEP8 Style Guide](https://www.python.org/dev/peps/pep-0008/) - Write all your python code according to this format, forever. The strength of Python is actually in readibility and accessibility, *not* raw computing power (C or FORTRAN has Python beat in these respects). The idea is that *development time* spent writing and debugging is much more than *computational run time*, so writing modular, systematic, and well-commentated code will overall save more man-hours than just going for raw power.  If code is written and commentated poorly, then this advantage is lost.
