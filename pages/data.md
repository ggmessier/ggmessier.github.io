---
layout: default
use_math: true
---
# Data Analytics

*It’s tough to make predictions, especially about the future.*

-Yogi Berra

Data analytics, machine learning and artificial intelligence are very hot topics.  [Andrew Ng](https://en.wikipedia.org/wiki/Andrew_Ng) has a nice summary of the current state of AI [here](https://youtu.be/NKpuX_yzdYs).  The purpose of these pages is to document some of the practicalities of implementing machine learning as I work through them as part of my research.


## Background Material

- **Andrew Ng's Stanford Grad Course:** You can access all of his 2008 Stanford video lectures on [YouTube](https://www.youtube.com/playlist?list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN).  Note that YouTube also has videos shot in 2008 from Ng's grad course that start with [this one](https://youtu.be/UzxYlbK2c7E).  The material in these two lecture series overlap a fair bit but the 2008 lectures are a bit dated.  In particular, they have almost no content on neural networks.  Also useful are the [course notes](http://cs229.stanford.edu/syllabus.html) from Ng's CS229 graduate course at Stanford.

## Development Platform

Our machine learning work is done using numerical python ([NumPy](http://www.numpy.org/)) attached to a mySQL database front-end.  The machine learning algorithms are implemented and tested using NumPy and the raw data is contained in the database.  If you're a student in my research lab, it's assumed you're doing your work on an Ubuntu linux PC.

### MySQL

[MySQL](https://www.mysql.com/) is an open source [relational database](https://en.wikipedia.org/wiki/Relational_database) maintained by Oracle that implements its interface using the standardized structured query language (SQL).  MySQL utilizes a client/server model where the server is responsible for the database and the client accesses data from the database by sending SQL queries to the server.  While there are an uncountable number of MySQL references on the web, a good place to start is [this tutorial](https://downloads.mysql.com/docs/mysql-tutorial-excerpt-5.5-en.pdf).

The python client we utilize is [pymysql](https://github.com/PyMySQL/PyMySQL) which comes standard both with most Linux distributions and Mac Ports.  This allows a python program to make queries to a MySQL server and load database data directly into python data structures (lists, arrays, etc.).

If you're just learning SQL queries, the [MySQL Workbench](https://dev.mysql.com/downloads/workbench/) program is a nice tool that allows you to connect to a MySQL server, submit SQL queries and see the results in a table format.  This is a really good way to test to make sure your queries work before implementing them in python. 

### Python

Your python programs should make use of the numerical python (NumPy), scientific python (SciPy) and matplotlib libraries.  All of these can be installed using Mac ports or your linux distribution (ie. using ``apt-get``).  It's useful to do your development within [Eclipse](http://www.eclipse.org) using the [PyDev](http://www.pydev.org/) development extension.  In particular, PyDev allows you to use a debugger within the eclipse environment.

### Working with Raw Data

Often when working with raw data, it is necessary to search for text strings that contain certain characters or patterns.  For example, when working with Retrosheet baseball data, any event string that starts with an "S" represents a single hit, any string that contains the characters "-H" one or more times represents one or more runs reaching home, etc.  When performing text string analysis and pattern matching, both python and SQL queries allow for the use of the very powerful *regular expression* text parsing language.  There are a vast number of regular expression tutorials on the web but a very good and comprehensive tutorial can be found [here](https://www.princeton.edu/~mlovett/reference/Regular-Expressions.pdf).


## Model Selection

While understanding the theory of various learning algorithms is straightforward, knowing how to tune the parameters of those algorithms to best suit a particular data set is the "secret sauce" of using the algorithms effectively.  Ng provides some *excellent* insight on how to do this in the videos of Section 10 of his [lecture series](https://www.youtube.com/playlist?list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN).

### Model Parameter Selection

To start, randomly allocate 60% of the data to the training set, 20% to the cross-validation (CV) set and 20% to the test set.  The size of the CV and test sets will remain the same but the size of the training set, $m$, can vary in order to generate learning curves.

Once the model and value of $m$ are set, data for the three sets are randomly selected and values for $J(\theta)$, $J_{\rm train}(\theta)$, $J_{\rm CV}(\theta)$ and $J_{\rm test}(\theta)$ are calculated.  Since the data is selected at random, consider doing a few iterations here and using averages to calculate the error values.

Current strategy:
- Using the full training set:
  - Consider polynomials of power 1 through 5 with regularization parameter $\lambda=$ and select with one with the best cross validation error.
  - Consider regularization parameters $\lambda = 0.01$ through $10.24$ (increasing by factors of 2) and select the one with the best cross validation error.

- Generate a learning curve for a range of $m$ values 



## Baseball Data

It's nice to have a dataset to practice machine learning techniques and the baseball community provides a *huge* amount of data on major league baseball (MLB) games.  In particular, a group of very committed volunteers maintains the [Retrosheet](http://retrosheet.org) project where the outcome of every at-bat in every MLB game going back to 1921!  In addition to Retrosheet, there is even more data that can be downloaded directly from the MLB servers.  In particular, MLB provides access to the pitchf/x system data that contains detailed information on every pitch thrown in the MLB since 2008 (speed, ball rotation, movement, pitch type, etc.).

While the Retrosheet data is more than sufficient for testing whatever machine learning algorithm you're interested in, a good overview of all the data available for download can be found  on the [SABR website](https://sabr.org/sabermetrics/data).

### Baseball on a Stick (BBOS)

While it is possible to download the play-by-play event files for games directly from Retrosheet [here](https://www.retrosheet.org/game.htm), you would spend a fair bit of time loading them into a MySQL database.  The [BBOS](https://sourceforge.net/projects/baseballonastic/) program does this work for you and delivers a MySQL database populated with any year of Retrosheet data you'd like.  This software downloads both pitchf/x data and retrosheet data.

For Linux/Mac people, this package only works on Windows.  My work-around was to run BBOS in a windows virtual machine on my Mac and have it populate a MySQL database running on OSX.  Also, there's a bug in the package that prevents it from working with MySQL 5.7 but the fix is discussed in [this post](https://sourceforge.net/p/baseballonastic/discussion/820145/thread/0f201970/?limit=25#f99d).

Once you've populated your Retrosheet database, the table with all the play-by-play data is ``events``.  The table that links player ID's to their names and positions is ``rosters``.


### Working with Retrosheet

Let's assume that we want to start with a supervised learning algorithm.  How do we translate the Retrosheet data to the training set $x$ and observation vector $y$?  There are many ways to do this but one way is to treat each individual player as a single observation where the size of our training set, $m$, is the number of players in the MLB.

You can then choose what you would like your algorithm to determine.  Perhaps you'd like to predict the offensive impact of a player (RBI's+runs) in a particular week based on the performance of previous weeks.  

If so, you will first need to mainipulate the database to get a timeline of the offensive performance and all the possible input features you'd like to consider for your algorithm.  Note that you should gather as many features as possible at this stage since you'll reduce them later in the design process.

At this point, you will be working with a combination of SQL queries and a python program to consolidate the data.  The SQL queries will give you a single entry per at-bat in every game and your python program will use this data to populate an offensive timeline for each unique player.  At this point, you will be getting much of your information from the ``event_tx`` field which corresponds to the retrosheet [event field](https://www.retrosheet.org/eventfile.htm).  Using regular expressions is super handy for decyphering these event strings.

Once you have your offensive event timelines, you can decide how to convert them into a training set $x$ and observation vector $y$.  One option is to use a time window of a certain number of weeks, average or sum each feature over that window and use that training data to predict the offensive impact of a player in the following week.  This is useful for fantasy baseball leagues that allow you to change your roster once per week.











