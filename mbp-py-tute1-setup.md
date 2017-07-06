# Tutorial 0: Getting Set Up for Python

*Prepared for the Monash Bioinformatics Platform*

Much of the content from this page comes from [here](https://github.com/ehmatthes/intro_programming) and [here].

### 1. Get Python (Obviously)
First, you'll need to get Python. At the time of this writing, there are two "generations" of Python: Python 2.7 and Python 3.6. Python 2.7 chronologically came first, and Python 3.6 came along later as the next generation with massive code overhauls. By and large, Python 2.7 still persists because many older systems were built with it, and organizations have found it extremely difficult to do a massive upgrade to Python 3.6. In any case, if you're just starting out, go with Python 3.6 (no point learning an older version!). 

(Segway on version numbers: when we write "`python x.y`", *x* is the "generation" number, i.e. Python 2 or Python 3, and *y* is the update number, where smaller, iterative updates were applied within the same generation.)

Python should have already been installed if you're using a Mac. To check if you have it installed:
 - Go to `Applications` --> `Terminal` to open a command line interface (CLI). 
 - Type `python`. This actually starts up Python. 
 
On my computer, I see something like:

```
$ python
Python 2.7.13 (v2.7.13:a06454b1afa1, Dec 17 2016, 12:39:47) 
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

A few pointers:
 - The dollar symbol in the first line, `$ python`, is a bit of writing convention to indicate to readers that this line is to be typed into a CLI, so don't actually type "`$ python`". Just "`python`" will do. 
 - This actually starts up Python 2.7. If I want Python 3, I type:

```
$ python3
Python 3.5.1 (v3.5.1:37a07cee5969, Dec  5 2015, 21:12:44) 
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

### 2. Get Homebrew
If Python 3 hasn't been installed on your computer, use [Homebrew](https://brew.sh/) to install it (and even if you already have Python 3, get `Homebrew` anyway!). `Homebrew` is a package manager for OSX, meaning that it puts software in meaningful places so that the computer knows where to find it. First you'll need Apple's Xcode. Again, in your terminal, run the command:

```
xcode-select --install
```

And then install `Homebrew` itself using:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once its completed installing, use it to install Python3:

```
brew install python3
```

### 3. Get an Integrated Developer Environment (IDE)
An [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) is a fancy name for something like the Microsoft Word program, but for people to write code in. The same way that Microsoft Word has features like spell checks, an IDE will have similar syntax-checking features to alert programmers when they've typed something wrong. 

My personal favourite is [Jupyter](http://jupyter.org/). I've also been recommended [Sublime Text](http://www.sublimetext.com/3), which is more like a text editor. Unfortunately, Sublime Text is not free (though there's a free trial), but Jupyter is. Sublime Text is a straightforward download; getting Jupyter is a little more complicated - you'll have to `pip install` it. Which brings us very nicely to...

### 4. Get PIP Installer
The `pip installer` automatically installs Python libraries (a.k.a. "modules", "packages", "add-ons") in a place where your installation of Python knows where to find. To get the `pip installer` itself:

```
curl -O http://python-distribute.org/distribute_setup.py
python distribute_setup.py
curl -O https://raw.github.com/pypa/pip/master/contrib/get-pip.py
python get-pip.py
```

We'll install Jupyter as an example of how to use the pip installer. There's really not much to it:

```
pip3 install jupyter
```

That's the end of this tutorial. 
