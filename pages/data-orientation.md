---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# New Student Orientation

This page will provide a series of exercises meant to bring new research students up to speed on some of the data tools I use in my research group.  This page assumes that you have cloned a local copy of my [public data analysis repository](https://github.com/ggmessier/data-analytics).  References to files and directories will be relative to the root directory of this repository.

## Data Set
Much of my data work involves analyzing and visualizing the timelines of individuals who interact with health services and/or emergency social supports.  This is very sensitive data and can only be accessed under security and privacy protocols that are approved by the University of Calgary [ethics review boards](https://research.ucalgary.ca/conduct-research/ethics-compliance).  In other words, it is not possible to share it here.

In order to have a dataset that we can use here to learn about data analytics, I have "disguised" a public domain dataset to appear as though it represents individuals who are interacting with mental health, police and emergency shelter services.  Each individual is linked with one or more timestamped events of the following type:
- **Referral:** Referral to a treatment or support program.
- **Stay:** A stay in an emergency shelter or hospital.
- **Major Event:** An event with a significant negative effect on an individual (ie. police interaction, emergency room visit, etc.).
- **Adverse Outcome:** An adverse outcome that we're trying to use our data analysis to detect, predict and/or avoid (ie. overdose, incarceration, etc.).

Broadly speaking, we want to use these timestamped events to identify individuals at risk of having their first adverse outcome or a repeat adverse outcome.

If you are interesting in finding out who the individuals *actually* are in our data set, [click here](data-baseball).

## Exploratory Data Analysis
Exploratory data analysis (introduced in Chapter 4 of [Seltman's book](http://www.stat.cmu.edu/~hseltman/309/Book/Book.pdf)) is a *very* important and often overlooked aspect of machine learning and data analysis.  In order for your algorithm to produce good results, you must first understand the nature of your data and see if it contains any obvious inconsistencies or errors.  Exploratory data analysis (EDA) is essentially using relatively straightforward plots and statistical quantities to determine this.

Some EDA for our dataset is contained in `orientation/Exporatory Data Analysis.ipynb`.



<br>
<br>
  
