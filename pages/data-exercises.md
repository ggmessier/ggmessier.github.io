---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# Exercises & Demos

This page provides data sets and a series of exercises related to the techniques I use in my research group.  This page assumes that you have cloned a local copy of my [public data analysis repository](https://github.com/ggmessier/data-analytics).  References to files and directories will be relative to the root directory of this repository.

## Data Set
Much of my data work involves analyzing and visualizing the timelines of individuals who interact with health services and/or emergency social supports.  This is very sensitive data and can only be accessed under security and privacy protocols that are approved by the University of Calgary [ethics review boards](https://research.ucalgary.ca/conduct-research/ethics-compliance).  In other words, it is not possible to share it here.

In order to have a dataset that we can use here to learn about data analytics, I have "disguised" a public domain dataset to appear as though it represents individuals who are interacting with mental health, police and emergency shelter services.  Each individual is linked with one or more timestamped events of the following type:
- **Referral:** Referral to a treatment or support program.
- **Stay:** A stay in an emergency shelter or hospital.
- **Major Event:** An event with a significant negative effect on an individual (ie. police interaction, emergency room visit, etc.).
- **Adverse Outcome:** An adverse outcome that we're trying to use our data analysis to detect, predict and/or avoid (ie. overdose, incarceration, etc.).

Broadly speaking, we want to use these timestamped events to identify individuals at risk of having their first adverse outcome or a repeat adverse outcome.

If you are interesting in finding out who the individuals *actually* are in our data set, [click here](data-baseball).

## Notebooks

Before looking at these notebooks, be sure you've read the relevant [background material](data-background).


- `demo/Exporatory Data Analysis.ipynb` introduces some EDA techniques and also demonstrates some of the properties of our data set.

- `demo/Survival Analysis.ipynb` demonstrates survival functions and Cox proportional hazards linear regression using scikit-learn libraries.







<br>
<br>
  
