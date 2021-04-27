---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# Development Environment


All of the tools we use in my group are open source and can be downloaded and used for free.  If you have the time, consider joining an open source development community to give back to the amazing array of tools that are available.  It makes the data science community better and is excellent experience when it comes time to apply for a job.

## Operating System
It is essential that you do your development and run your simulations on the linux operating system.  [Ubuntu](https://ubuntu.com/) is the best choice simply because it's so common and most software packages are tested on it.  **Note:** Be sure you're using a native installation and not running Linux inside a virtual machine.  A virtual machine installation will not give you the performance or stability that you will need.


## Python
Most of our data work is done using python.  If you need a general introduction to python, I like [The Quick Python Book](https://www.amazon.ca/Quick-Python-Book-Naomi-Ceder/dp/1617294039) which can be read for free through the University of Calgary library.  However, there are an uncountable number of good Python tutorials and introductions on the web.


## Pandas
We make heavy use of the [Pandas](https://pandas.pydata.org/) python data analysis library.  The library is designed to efficiently store and manipulate data tables.  It provides much of the functionality available in SQL in terms of being able to join tables, perform operations by grouping data keys, etc.  Start with the [getting started](https://pandas.pydata.org/docs/getting_started/index.html) pandas documentation (in particular "10 minutes to pandas").  The [full users guide](https://pandas.pydata.org/docs/user_guide/index.html) is more useful as a reference when you encounter specific problems during your software development work.

## Other Python Libraries
In addition to pandas, we also make use of the [NumPy](https://numpy.org/), [matplotlib](https://matplotlib.org/) and [SciPy](https://www.scipy.org/) libraries.  It's not necessary to become proficient with these right away.  Just scan the introductory material and be aware of them as a resource for when you start your research work.

We also make use of the [scikit learn](https://scikit-learn.org) machine learning library.  This is a good general purpose library with most of the important machine learning algorithms.  scikit is a great place to start for your project but you may find that you move to more specialized libraries as you get deeper into your project.

## Jupyter Notebooks
[Jupyter](https://jupyter.org/) notebooks are a mechanism for combining python code, plots and notes created using the [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) language.  Think of them as a very super-powered replacement for a log book that are very popular in the data science community.  I prefer to run the Jupyter "lab" interface rather than the "notebook" interface since it does a better job of also handling plain python files.

We do most of our exploratory development using notebooks and tend to transition to pure python code once we've got something ready for a library or need to transition to pure python for advanced debugging purposes.

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
An important part of research is writing about your results.  For your thesis and all technical papers, you will be using [latex](https://www.latex-project.org/).  Many of us code latex directly in a text editor and compile it on the command line.  However, if you want a more sophisticaled editor, [Overleaf](https://www.overleaf.com/) is popular and the Overleaf website also has some good tutorials.  For drawing diagrams, [Inkscape](https://inkscape.org/) is a good choice.

Be sure to also check out my page on [effective technical writing](writing).



<br>
<br>