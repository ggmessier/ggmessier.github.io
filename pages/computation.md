---
layout: default
---

# Help!  Dr. Messier needs to give me a faster computer!

If you find that you're spending a lot of time waiting for your simulations to finish, answer the following questions.


## Am I generating too many points?

Often, you will be using your simulation or machine learning algorithm to generate the data points of a figure or to examine different parameter settings on an algorithm to determine its best point of operation.  If you're doing this, follow this procedure:

1. Use your judgement to set an appropriate maximum and minimum value for the x-axis of your graph or the settings for the parameter you're tuning.  Discuss this with Dr. Messier if you're having trouble decising.

1. **Generate a maximum of 3 points between your minimum and maximum.**  This means you should be generating 5 points in total.  If your results look good or indicate you need a higher resolution, you can come back later to fill in more points.


## Am I using too much data?

Most administrative datasets are not as large as many datasets in the general machine learning domain.  However, they can still get pretty large.  When generating preliminary results, it's fine to run your code on a subset of your data to make sure everything is working as you expect.

Discuss this with Dr. Messier but here are some rules of thumb for how big your data set should be when generating initial results:
- 5-10 million entries (table rows)
- 5-10 data features (table columns)


## Is my code efficiently programmed?

When working with panda libraries, there are often many ways to write code that generate the same results.  However, these different approaches can often result in **very** different execution times.


### How slow is too slow?

In the early stages of your research, you should not be waiting longer than 15 minutes for any result.  Once your code is stable, generating the desired output and bug free, it's safe to run it for many hours or days to produce your final thesis/paper results.


### How do I know if my code is slow?

Always try to use [tqdm](https://tqdm.github.io/) progress bars.  This will allow you to see how quickly a particular code cell is executing.  If the progress bar is predicting the code is going to take too long, terminate it and see if you can make it faster.


### How do I make my code faster?

When working with python (or any scripted language), execution speed is greatly influenced by whether you're using built in library functions.  Loops can literally be made almost 100,000 times faster based on the coding choices you make.  An example is [provided here](https://towardsdatascience.com/how-to-make-your-pandas-loop-71-803-times-faster-805030df4f06) but this isn't the only strategy.  You may need to employ different strategies depending on your specific problem.  In almost all cases, a quick google will yield a discussion of how to improve your speed.


### Am I saving my intermediate results?

A lot of tasks that generate intermediate results (ie. pre-processing of a data table) only need to be done once and can then be saved to disk.  A very useful caching utility developed by our group can be found [here](https://github.com/ggmessier/data-analytics/blob/master/demo/Caching%20Intermediate%20Results.ipynb).












