---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# Development Environment


All of the tools we use in my group are open source and can be downloaded and used for free.  If you have the time, consider joining an open source development community to give back to the amazing array of tools that are available.  It makes the data science community better and is excellent experience when it comes time to apply for a job.

## Operating System

My team tends to use either the mac OSX or linux operating systems.  These are *far* more stable for scientific computing than windows (IMHO).  If you're using linux, [Ubuntu](https://ubuntu.com/) is the best choice simply because it's so common and most software packages are tested on it.  **Note:** Be sure you're using a native installation and not running Linux inside a virtual machine.  A virtual machine installation will not give you the performance or stability that you will need.


## Development Environment

The first step in installing all of the libraries and tools mentioned [here](./data-background.md) is to install [Miniconda](https://docs.anaconda.com/free/miniconda/index.html) on your computer.  This will install python and the `pip` installer that is necessary for installing the other packages.

Once miniconda is installed, you should install:
 1. jupyter lab
 1. pandas
 1. numpy
 1. sci-kit learn
 1. matplotlib

In all cases, google the installation procedure for each of these libraries/tools and use the `pip` method when available.

## Github
All code developed by my research group is managed using [GitHub](http://github.com).  This is good software development practice and allows members of our team to collaborate on a common code base.  Prospective software develoment and data science employers will often ask potential candidates if they have a GitHub portfolio of the code they worked on during their studies.


You will need to know how to:
- Clone a repository to create a local copy on your computer.
- Create a branch to work in.
- Commit changes to your branch.  **Note:** Commit changes only to mark development milestones.  Do not use daily commits as a way to "save your work".
- Potentially merge changes from the master branch into your branch.

A good resource is the [Pro Git](https://git-scm.com/book/en/v2/) book.  Concentrate on Chapters 1-3 and the relevant commands from appendix A3.  The [reference guide](https://git-scm.com/docs) is also handy.

You will need to install:
- The git command line tools.
- The [nbdime](https://nbdime.readthedocs.io/en/latest/) diff/merge tools for Jupyter notebooks.
- The `gitk` branch visualization tool.


## Latex
An important part of research is writing about your results.  For your thesis and all technical papers, you will be using [latex](https://www.latex-project.org/). I write latex directly in a text editor and compile it on the command line.  However, most students prefer [Overleaf](https://www.overleaf.com/) and the Overleaf website also has some good tutorials.  For drawing diagrams, [Inkscape](https://inkscape.org/) is a good choice.

Be sure to also check out my page on [effective technical writing](writing).



<br>
<br>