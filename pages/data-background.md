---
layout: default
use_math: true
---
# Background Material and Development Tools


## Reading & Videos

### New Students

The purpose of this section is to give students who are brand new to our group something to look at to get up to speed.  Here, I'm trying to strike a balance between giving you the fundamentals that everyone should know and not spending too much time exploring techniques that you might not use in your specific project.

- **Probability Lectures:**
  + It's impossible to understand how machine algorithms work without a background with probability and statistics.
  + The lectures for my probability grad course are on [YouTube](https://youtube.com/playlist?list=PL7sWxFnBVJLUbrCHertPLEqqCyLVnG-tN).  Lectures 1-4 are basically undergrad material but good to review.  The multi-variate material in Module 6 and 7 is important to cover.  The rest of the lectures aren't important.

- **Andrew Ng's Stanford Grad Course:**
  + Andrew Ng is a giant in the field of machine learning and he has many hours of great lectures on YouTube.
  + His full 2017 Stanford University lectures are posted [here](https://www.youtube.com/playlist?list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN).
  + All of these lectures are worth watching but, if you're a new student, you should start with the introductory, basic linear algorithm and machine learning application material (Lectures 1.1-1.3, 2.1-2.8, 4.1-4.6, 6.1-6.7, 10.1-10.7, 11.1-11.5).

- **Textbooks:**
  + Part I of [Ian Goodfellow's Deep Learning book](https://deeplearningbook.org) is a good review of some of the foundational theory necessary to understand machine learning.  Don't worry about Parts II and III for now.
  + In [Elements of Statistical Learning](https://web.stanford.edu/~hastie/ElemStatLearn/), review Chapters 1 and 2 and Sections 3.1-3.3, 4.1-4.4, 7.1-7.5, 7.10 and 7.11.
  + Howard Seltman's [Experimental Design and Analysis](http://www.stat.cmu.edu/~hseltman/309/Book/Book.pdf) book has a good chapter on probability/statistics (Chapter 3) and a *very* good chapter on exploratory data analysis (Chapter 4).

### Existing Students

Everything in this section is really good but it may or may not be useful for you, depending on the focus of your project.

- **Neural Networks:**
  + Part II of Ian Goodfellow's [Deep Learning book](https://www.deeplearningbook.org/) is a good introduction into neural networks. [Michael Nielsen's book](http://neuralnetworksanddeeplearning.com/) also gives an accessible introduction into neural networks.
  + The two libraries we most often use for neural network coding are [Keras](https://keras.io/) and [scikit-learn](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.neural_network).  There are so many tutorials for both these libraries if you google them but Machine Learning Mastery (see below) is a good place to start for Keras.


- **Machine Learning Mastery:**  This is an [excellent website](https://machinelearningmastery.com) for all things machine learning but particularly [deep learning](https://machinelearningmastery.com/category/deep-learning/).  The site also has some good tutorials for [getting started with Keras](https://machinelearningmastery.com/tutorial-first-neural-network-python-keras/).

- **Andrew Ng's Original Machine Learning Lectures:**  Andrew's original 2008 lectures are [also posted](https://youtu.be/UzxYlbK2c7E).  They're a bit dated (very little neural network content) but he does place a different emphasis on certain topics.  If there's something that you didn't understand from a 2017 lecture, you might want to check here.



## Development Environment and Tools

All of the tools we use in my group are open source and can be downloaded and used for free.  If you have the time, consider joining an open source development community to give back to the amazing array of tools that are available.  It makes the data science community better and is excellent experience when it comes time to apply for a job.

### Operating System
It is essential that you do your development and run your simulations on the linux operating system.  [Ubuntu](https://ubuntu.com/) is the best choice simply because it's so common and most software packages are tested on it.  **Note:** Be sure you're using a native installation and not running Linux inside a virtual machine.  A virtual machine installation will not give you the performance or stability that you will need.


### Python
Most of our data work is done using python.  If you need a general introduction to python, I like [The Quick Python Book](https://www.amazon.ca/Quick-Python-Book-Naomi-Ceder/dp/1617294039) which can be read for free through the University of Calgary library.  However, there are an uncountable number of good Python tutorials and introductions on the web.


### Pandas
We make heavy use of the [Pandas](https://pandas.pydata.org/) python data analysis library.  The library is designed to efficiently store and manipulate data tables.  It provides much of the functionality available in SQL in terms of being able to join tables, perform operations by grouping data keys, etc.  Start with the [getting started](https://pandas.pydata.org/docs/getting_started/index.html) pandas documentation (in particular "10 minutes to pandas").  The [full users guide](https://pandas.pydata.org/docs/user_guide/index.html) is more useful as a reference when you encounter specific problems during your software development work.

### Other Python Libraries
In addition to pandas, we also make use of the [NumPy](https://numpy.org/), [matplotlib](https://matplotlib.org/) and [SciPy](https://www.scipy.org/) libraries.  It's not necessary to become proficient with these right away.  Just scan the introductory material and be aware of them as a resource for when you start your research work.

We also make use of the [scikit learn](https://scikit-learn.org) machine learning library.  This is a good general purpose library with most of the important machine learning algorithms.  scikit is a great place to start for your project but you may find that you move to more specialized libraries as you get deeper into your project.

### Jupyter Notebooks
[Jupyter](https://jupyter.org/) notebooks are a mechanism for combining python code, plots and notes created using the [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) language.  Think of them as a very super-powered replacement for a log book that are very popular in the data science community.  I prefer to run the Jupyter "lab" interface rather than the "notebook" interface since it does a better job of also handling plain python files.

We do most of our exploratory development using notebooks and tend to transition to pure python code once we've got something ready for a library or need to transition to pure python for advanced debugging purposes.

### Github
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


<br>
<br>