---
layout: default
use_math: true
---
# Background Material 

The purpose of this section is to give students who are brand new to our group something to look at to get up to speed.  Here, I'm trying to strike a balance between giving you the fundamentals that everyone should know and not spending too much time exploring techniques that you might not use in your specific project.

### Probability Lectures
- It's impossible to understand how machine algorithms work without a background with probability and statistics.
- The lectures for my probability grad course are on [YouTube](https://youtube.com/playlist?list=PL7sWxFnBVJLUbrCHertPLEqqCyLVnG-tN).  Lectures 1-4 are basically undergrad material but good to review.  The multi-variate material in Module 6 and 7 is important to cover.  The rest of the lectures aren't important.

### Andrew Ng's Stanford Grad Course
- [Andrew Ng](https://www.andrewng.org/) is a giant in the field of machine learning and he has many hours of great lectures on YouTube.
- His full 2018 Stanford University lectures are posted [here](https://www.youtube.com/playlist?list=PLoROMvodv4rMiGQp3WXShtMGgzqpfVfbU).
- All of these lectures are worth watching but, if you're a new student, you should start with lectures 1, 2, 3, 4, 8, 10 and 11.

### Textbooks
- Part I of [Ian Goodfellow's Deep Learning book](https://www.deeplearningbook.org) is a good review of some of the foundational theory necessary to understand machine learning.  Don't worry about Parts II and III for now.
- In [Elements of Statistical Learning](https://web.stanford.edu/~hastie/ElemStatLearn/), review Chapters 1 and 2 and Sections 3.1-3.3, 4.1-4.4, 7.1-7.5, 7.10 and 7.11.
- Howard Seltman's [Experimental Design and Analysis](http://www.stat.cmu.edu/~hseltman/309/Book/Book.pdf) book has a good chapter on probability/statistics (Chapter 3) and a *very* good chapter on exploratory data analysis (Chapter 4).


### Online Resources
- The standard classic ML library is [scikit-learn](https://scikit-learn.org/stable/index.html) and the [user guide](https://scikit-learn.org/stable/user_guide.html) is a very readable resource.
- [This is a very good wikipedia summary](https://en.wikipedia.org/wiki/Receiver_operating_characteristic) of many of the performance metrics we use.
- We also often work with imbalanced data sets which makes the [imbalanced-learn](https://imbalanced-learn.org/stable/) library and it's associated documentation important.
- Also related to imbalanced data is [this excellent article](https://towardsdatascience.com/imbalanced-data-stop-using-roc-auc-and-use-auprc-instead-46af4910a494) on the difference between AUROC and AUPRC.

### Development Resources
- All our development work is done in python.  For an introduction to the language, I like [The Quick Python Book](https://www.amazon.ca/Quick-Python-Book-Naomi-Ceder/dp/1617294039) which can be read for free through the University of Calgary library.  However, there are an uncountable number of good Python tutorials and introductions on the web.

- Our development environment is [Jupyter](https://jupyter.org/) notebooks which are a mechanism for combining python code, plots and notes created using the [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) language.  Think of them as a very super-powered replacement for a log book that are very popular in the data science community.  I prefer to run the Jupyter "lab" interface rather than the "notebook" interface since it does a better job of also handling plain python files.

- We also make extensive use of the following libraries:

  + The [scikit learn](https://scikit-learn.org) machine learning library is the standard for class (non-deep) machine learning models.  The [tutorials](https://scikit-learn.org/stable/tutorial/index.html) are useful but the [user guide](https://scikit-learn.org/stable/user_guide.html) is more focused.  If you're new to machine learning, go through sections 1.1.1, 1.1.11, 1.10, 1.11.1, 1.11.2, 1.17.1, 3 and 10.

  + The [Pandas](https://pandas.pydata.org/) library is designed to manipulate data in table form.  Start with the [getting started](https://pandas.pydata.org/docs/getting_started/index.html) pandas documentation (in particular "10 minutes to pandas").  The [full users guide](https://pandas.pydata.org/docs/user_guide/index.html) is more useful as a reference when you encounter specific problems during your software development work.

  + Most of our machine learning problems are *imbalanced* (there are many more negative cases than positive cases).  The [imbalanced learn](https://imbalanced-learn.org/stable/user_guide.html) library contains several algorithms for handling imbalanced problems.  If you're new, read sections 1, 2.1 and 7 to get started.

  + We also make use of the [NumPy](https://numpy.org/), [matplotlib](https://matplotlib.org/) and [SciPy](https://www.scipy.org/) libraries.  It's not necessary to become proficient with these right away.  Just scan the introductory material and be aware of them as a resource for when you start your research work.




<br>
<br>