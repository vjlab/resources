# PAML & Treesub

*Written by: Don Teng<br>
Last update: 15 June 2017<br>*

## [PAML](http://abacus.gene.ucl.ac.uk/software/paml.html)
...stands for *Phylogenetic Analysis by ML*. It has several uses, such as inferring ancestral sequences based on modern sequences. 

### Installation
This is actually quite easy. Get 2 versions:
1. The point-and-click interface, called `PamlX`. Download and install it as a normal bit of software. However, this really is only the interface - if you try to run it, it will ask where you've placed the executables. That's in step 2:
2. The executable file, which `treesub` requires. This isn't the download link at the top of the `PAML` site (that's the GUI), it's hidden somewhere in the middle.  Ctrl-F "For the MAC, we have compiled a version for MAC OSX". Fortunately, the Mac OS version has already been compiled, so it's ready to go after downloading (Linux or Windows users will have to continue with all that `Makefile` gibberish).

## Run
I've never ued PAML extensively before, except for its `codeml` module. That's in a separate tutorial.

## [Treesub](https://github.com/tamuri/treesub)
This is an extension which uses some `PAML` functions, stitched together with RAXML and FigTree. It's primarily useful for producing a tree which shows the amino acid substitutions along the branches. 

### Installation

You'll need to get:
1. RAxML (Not easy. See the *RAXML installation tutorial*)
2. PAML executable. I've verified this build on a MacOS X (High Sierra), paml 4.8.
3. The latest Java SDK version, which is currently 8. Get it [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
4. FigTree (easy)
5. The [Eclipse](https://www.eclipse.org/downloads/?) IDE, which is not actually used by `treesub`; you need it to get a `treesub.jar` application (the thing that you'll eventually double-click on to launch the program). 

**Procedure**
1. Download all the `treesub` files: download directly from Github, or `git clone https://github.com/tamuri/treesub`.
2. Open Eclipse, and open `build.xml` from inside the `treesub` folder.
3. Run the file, either from the taskbar at the top of the window (look for the button that has a "play" icon on it), or select Run > Run from the toolbar at the top. You should see some output being printed out like:

```
Buildfile: /Users/dten0001/Documents/clones/treesub/build.xml
clean:
makedir:
    [mkdir] Created dir: /Users/dten0001/Documents/clones/treesub/build
    [mkdir] Created dir: /Users/dten0001/Documents/clones/treesub/docs/api
    [mkdir] Created dir: /Users/dten0001/Documents/clones/treesub/dist
compile:
    [javac] /Users/dten0001/Documents/clones/treesub/build.xml:29: warning: 'includeantruntime' was not set, defaulting to build.sysclasspath=last; set to false for repeatable builds
    [javac] Compiling 8 source files to /Users/dten0001/Documents/clones/treesub/build
    [javac] Note: /Users/dten0001/Documents/clones/treesub/src/treesub/gui/AnnotatorGUI.java uses or overrides a deprecated API.
    [javac] Note: Recompile with -Xlint:deprecation for details.
jar:
      [jar] Building jar: /Users/dten0001/Documents/clones/treesub/dist/treesub.jar
dist:
BUILD SUCCESSFUL
Total time: 1 second
```

3. This will create a `treesub.jar` executable, which you can launch the point-and-click interface from. This will be inside `.../treesub/dist/treesub.jar`.

For those familiar with Java, my guess is that this is a Java file that needs to be locally compiled.

### Run
1. Double-click on the `treesub.jar` file to launch it, like you would a normal application. 
2. Fill in the fields where you installed the `RAXML` and `PAML` executables. `PAML` comes with a lot of files; look for `/paml<version number>/bin/baseml`.

The rest of the run instructions are on the `treesub` repo itself. 
