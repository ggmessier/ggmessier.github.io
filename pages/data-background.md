---
layout: default
use_math: true
---
# Background Material 

## Introductory Material

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

## Additional Resources

Everything in this section is really good but it may or may not be useful for you, depending on the focus of your project.

#### Neural Networks and Deep Learning

- Part II of Ian Goodfellow's [Deep Learning book](https://www.deeplearningbook.org/) is a good introduction into neural networks. [Michael Nielsen's book](http://neuralnetworksanddeeplearning.com/) also gives an accessible introduction into neural networks.

- The two libraries we most often use for neural network coding are [Keras](https://keras.io/) and [scikit-learn](https://scikit-learn.org/stable/modules/classes.html#module-sklearn.neural_network).  There are so many tutorials for both these libraries if you google them but Machine Learning Mastery (see below) is a good place to start for Keras.

- [Machine Learning Mastery](https://machinelearningmastery.com) is an excellent website for all things machine learning but particularly [deep learning](https://machinelearningmastery.com/category/deep-learning/).  The site also has some good tutorials for [getting started with Keras](https://machinelearningmastery.com/tutorial-first-neural-network-python-keras/).

#### Andrew Ng

- Andrew's original 2008 lectures are [also posted](https://youtu.be/UzxYlbK2c7E).  They're a bit dated (very little neural network content) but he does place a different emphasis on certain topics.  If there's something that you didn't understand from a 2017 lecture, you might want to check here.

#### Exploratory Data Analysis (EDA)
EDA (introduced in Chapter 4 of [Seltman's book](http://www.stat.cmu.edu/~hseltman/309/Book/Book.pdf)) is a *very* important and often overlooked aspect of machine learning and data analysis.  In order for your algorithm to produce good results, you must first understand the nature of your data and see if it contains any obvious inconsistencies or errors.  Exploratory data analysis (EDA) is essentially using relatively straightforward plots and statistical quantities to determine this.


#### Performance Metrics
There are a variety of metrics used to evaluate the performance of a classification algorithm.  I have some notes [here](data-metrics) that expand on this topic.

#### Survival Analysis
Much of our work is using machine learning algorithms to predict adverse future outcomes using features that have been accumulated in an individual's data record.  A related technique commonly used by medical researchers and bio-statiticians is survival analysis.  Survival analysis looks for features in the data that increase the risk of an adverse outcome.  It makes a series of very specific assumptions about the time to the occurence of these outcomes and whether they are censored by the end date of a study.

Some background reading:
- The [scikit survival analysis library](https://scikit-survival.readthedocs.io/en/latest/user_guide/understanding_predictions.html) also has some good background information.
- Some background notes that I've made are [here](data-survival).  
- These [lecture notes](https://data.princeton.edu/wws509/notes/c7.pdf) are well done but you don't have to understand the whole thing if you're just getting started.  Focus on 7.1 and 7.3.2.
- A more complete discussion of this topic is provided by the books by [Klein and Moeschberger](https://link.springer.com/book/10.1007/978-1-4757-2728-9), [Hoesmer, et. al.](https://onlinelibrary.wiley.com/doi/book/10.1002/9780470258019), [Guo](https://oxford.universitypressscholarship.com/view/10.1093/acprof:oso/9780195337518.001.0001/acprof-9780195337518).  You can probably read these for free if you have university library priviledges.





<br>
<br>