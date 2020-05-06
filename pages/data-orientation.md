---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# New Student Orientation

This page will provide a series of exercises meant to bring new research students up to speed on some of the data tools I use in my research group.  While you will likely end up using different data for your research project, these pages utilize publically available baseball data downloaded from the amazing [Retrosheet](http://www.retrosheet.org) website. I used the Baseball on a Stick code to create my baseball database, as I describe [here](data-baseball).

## How to Read this Orientation

There is a *lot* of information on this page.  Do not try to learn absolutely everything at first.  Start by spending a day scanning these resources, spending a day becoming generally familiar with the content and then start working on the tasks set out in the Exercises sections.  These exercises are meant to focus you on the main skills you'll need to start your research.  You can then re-visit the resources on this page as you encounter specific problems that require a particular tool.


## Your Operating System

All of our development is performed using linux and I recommend using the [Ubuntu](https://ubuntu.com/) since it's widely used and there's lots of online support available.  We make heavy use of linux libraries and tools so you will not be able to use windows. 


## Github

All code developed by my research group is managed using [GitHub](http://github.com).  This is good software development practice and allows members of our team to collaborate on a common code base.  I also use it as a platform to share open source code under the [GNU General Public License, Version 3](https://www.gnu.org/licenses/gpl-3.0.en.html).  The purpose of sharing our code is to provide the details regarding how we generate our research results and to allow the not-for-profit homelessness serving sector to utilize our work.  Finally, prospective software develoment and data science employers will often ask potential candidates if they have a GitHub portfolio of the code they worked on during their studies.  So, it also helps in the job hunt.

This orientation will require you to perform a series of exercises using different data analysis software tools and libraries.  The "solution" code for all these exercises can be found in the `baseball\orientation` folder of my public data analytics repository.  You can view this repository by hitting the "View on GitHub" button at the top of this page.



## The Baseball Data

In order to understand the purpose behind the exercises in this orientation, it's necessary to have a basic understanding of how the game of baseball is played.  Here are some of the many resources available that describe the game:

- [Wiki-How Baseball Tutorial](https://www.wikihow.com/Play-Baseball)
- [Quick Baseball Guide](https://www.tutorialspoint.com/baseball/baseball_quick_guide.htm)
- [The Rules of Baseball - EXPLAINED! (Video)](https://www.youtube.com/watch?v=skOsApsF0jQ)
- [Baseball Explained in 5 Minutes (Video)](https://www.youtube.com/watch?v=I8VGW0C_GO4)

You will be working with two tables.  The first is `Games` which contains an entry for every at-bat in every game played in 2018.  The fields in this table are:

  - `Time`: A timestamp that starts at 12pm (first game), 3:05pm (second game), 6:10 (third game).  Increments by 6 minutes for every at bat (based on average 3.5 batters/inning and 20min innings).
  - `GameId`
  - `Inning`
  - `TopBottom`
  - `PlayerId`
  - `Position`: Batter, Catcher, FirstBase, SecondBase, ThirdBase, ShortStop, LeftField, CenterField, RightField
  - `Event`: 
   - Event values for Batter: StrikeOut, PutOut (out because of a defensive play), Walk, Hit, Run, Steal 
   - Event values for defensive positions: Out, Error (player assigned an error)
  - Fields associated with Batter:
    - `PitchCount`: Number of pitches thrown during the at bat.
    - `Rbi`: Number of runners that score as a result of a player's hit.
    - `StartBase`: 1 - 4 where home base is 4.
    - `EndBase`
  - Fields associated with defensive positions:
    - `Outs`: Number of outs resulting from the defensive play.
    - `Players`: Number of players involved (one if the player got the out by himself).

The second table is `Rosters` which contains the full names and positions of each player indexed by `PlayerId`.


## SQL

It is possible that you will be provided with a dataset for your research in the form of a flat file perhaps in comma seperated value (CSV) format or [hierarchical data format](https://en.wikipedia.org/wiki/Hierarchical_Data_Format).  However, this data will almost always originate from some kind of [relational database](https://en.wikipedia.org/wiki/Relational_database) that is maintained by the organization collecting the data.  You may have to work with these databases directly as part of your research and you will certainly work with them if you pursue a career in data science.

The most popular way to interact with modern databases is using some variant of  [structured query language (SQL)](https://en.wikipedia.org/wiki/SQL).  The variant we work with in our group is [MySQL](https://www.mysql.com/), which is an open source variant of SQL maintained by Oracle.  While there are an uncountable number of MySQL references on the web, a good place to start is [this tutorial](https://downloads.mysql.com/docs/mysql-tutorial-excerpt-5.7-en.pdf).


### SQL Server Setup & DBeaver

For practice, I have set up a MySQL server that contains baseball data for the 2018 season.  This server is for use by my research group only so contact me directly for information on how to connect to it.

One of the pieces of information I will need is the IP address of your home computer.  To determine that, you can click [here](http://ipv4.whatismyv6.com).

While it is possible to interact with a MySQL server using a terminal program, as described in the tutorial, it is more common to interact with a database using a database browser or studio tool.  The program we will use is the community edition of the multi-platform [DBeaver](https://dbeaver.io) tool.  Documentation for how to use DBeaver is found [here](https://github.com/dbeaver/dbeaver/wiki).  You can focus on the "General User Guide" sections only.

### SQL Exercises

Using the information from Dr. Messier, create a connection to the MySQL server within DBeaver and then open and browse the `Events` and `Rosters` tables.  Once you verify you can view the data in the tables, write a series of SQL queries to do the following:

1. Determine how many games have been played in total during the season?
1. Determine how many home games were played by the New York Yankees?
1. Determine how many away games were played by the Toronto Blue Jays?
1. Determine what player has hit the most RBI's? 
1. Create a table of all hits generated in each game.  The table columns should be `Time`, `FirstName`, `LastName`, `PlayerTeam`.  This will require you to join the tables together.  [This](https://www.javatpoint.com/mysql-join) is a good summary of MySQL table join operations.
1. Determine the total number of hits scored in the 2018 season.
1. Determine the total number of hits scored in the 2018 season by players with last name ending in "ez".


To solve the last exercise, you'll need to use the regular expression functionality built into MySQL.  Regular expressions are a very powerful string parsing language that is available in a variety of programming languages (including python).  There are a vast number of regular expression tutorials on the web but a very good and comprehensive tutorial can be found [here](https://www.princeton.edu/~mlovett/reference/Regular-Expressions.pdf).  This document is quite long so here's a [more succinct summary](https://cs.lmu.edu/~ray/notes/regex/) that I've found helpful.  There's also a useful [online regex testing engine](https://regex101.com/) for experimenting with your own test strings as you learn the syntax.


## Python

We use SQL primarily for extracting data from databases.  The bulk of our data work is done using python.  If you need a general introduction to python, I like [The Quick Python Book](https://www.amazon.ca/Quick-Python-Book-Naomi-Ceder/dp/1617294039) which can be read for free through the University of Calgary library.


### Pandas

We make heavy use of the [Pandas](https://pandas.pydata.org/) python data analysis library.  The library is designed to efficiently store and manipulate data tables.  It provides much of the functionality available in SQL in terms of being able to join tables, perform operations by grouping data keys, etc.  Start with the [getting started](https://pandas.pydata.org/docs/getting_started/index.html) pandas documentation (in particular "10 minutes to pandas").  The [full users guide](https://pandas.pydata.org/docs/user_guide/index.html) is more useful as a reference when you encounter specific problems during your software development work.

### Other Python Libraries

In addition to pandas, we also make use of the [NumPy](https://numpy.org/) and [SciPy](https://www.scipy.org/) libraries.  It's not necessary to become proficient with these right away.  Just scan the introductory material and be aware of them as a resource for when you start your research work.

### Jupyter Notebooks

[Jupyter](https://jupyter.org/) notebooks are a mechanism for combining python code, plots and notes created using the [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) language.  Think of them as a very super-powered replacement for a log book that are very popular in the data science community.

We do most of our exploratory development using notebooks and tend to transition to pure python code once we've got something ready for a library or need to transition to pure python for advanced debugging purposes.


### Eclipse

[Eclipse](https://www.eclipse.org/). is the multi-platform software development environment of choice for many programming languages.  You will require the [PyDev](https://www.pydev.org/) eclipse extension.  If you're working through this orientation for the first time, don't worry about installing eclipse right away.  It will come in handy mainly as you start to develop a considerable amount of code as part of your research work.


### Streamlit

An important part of working with data is being able to develop interactive tools that respond in real time to user input.  This allows us to adjusting a range of variables (using things like buttons, lookup menus and slider bars) to see how this affects algorithm behaviour and visualizations.  These tools are useful for testing and presenting results to a range of audiences.  We use the [Streamlit](https://www.streamlit.io/) library for this.


### Visualization

An important part of data analytics is plotting data, particularly when troubleshooting and testing algorithms.  We use a combination of libraries for this:

- When making "quick and dirty" plots, the [built-in pandas visualization](https://pandas.pydata.org/docs/user_guide/visualization.html) capabilities are usually best.

- The pandas visualization mostly makes use of the [matplotlib](https://matplotlib.org/) library.  It's useful to be familiar with matplotlib both to better understand pandas plotting and as a stand-alone resource for generating very specific plots.  In general, matplotlib is a good library for generating static plots with lots of formatting controls that are good for creating figures for publication.

- A much more interactive visualization library is [Plotly](https://plotly.com/python/).   These plots tend to look great but the custom formatting options are a bit more limited than matplotlib.

While matplotlib and plotly can both be used in any python program, matplotlib is generally suited for the more static plots we generate in jupyter notebooks and plotly is better suited to a more interactive streamlit application.

### Python Exercises

- Install jupyter notebooks and have a look at the `Pre-Process Retrosheet Data` notebook posted in the `baseball\notebooks` directory on github.  I wrote this notebook to convert the retrosheet data tables into the `Games` and `Rosters` tables you worked with in the SQL section.  You don't have to fully understand this code.  Just treat it as an example of what a notebook can look like.

- Create a new notebook called `Orientation Exercises` and work through the following exercises:

1. In DBeaver, export the `Games` table in CSV format and read the table into your notebook.  Display the table to ensure the fields imported correctly.   Save the `Games` table in HDF format and delete the CSV file.  HDF format is a more compact and efficient format that you should use whenever you need to store intermediate results to disk.  Modify your notebook to read the `Games` table from the HDF file at the start of your notebook.

2. Add a new column to the data table called `LongGameId` which contains a unique game ID string with the following format:

    ```
    <Home Team Abbreviation> + <Away Team Abbreviation> + <Year> + <Month Number> + <Day> + <Daily Game Number (1 for first game of the day, 2 for second, etc.>
    ```

3. Determine the average number of outs per game for all the different fielder positions except for the pitcher.  For hitters, determine the number of times the hitter gets on base, the number of runs the hitter scores and the number of RBIs credited to the hitter averaged over the number of plate appearances (at bats).

4. Understanding the `groupby()` function is important when creating summary statistics for groups of data records (e.g. all data records for a team, all data records for a unique player, etc.).  Use this function to create a summary of each player that includes:
  - The player's fielder position (defined as the position the player is assigned most often).
  - Number of games played in the season.
  - Number of at bats in the season.
  - Average number of outs per game the player is involved in as a fielder.
  - Average times the player gets on base as a hitter per at bat.
  - Average runs the player scores per at bat.
  - Average RBIs the player generates per at bat.
Also use the function to create a summary of each game that includes:
  - Home team abbreviation.
  - Away team abbreviation.
  - Team abbreviation of the winner.
  - Team abbreviation of the loser.
  - Final score for the winner.
  - Final score for the loser.
  - The minimum lead in number of runs maintained by the winner during the game.  This number will be negative if the winner fell behind the other team during the game.
  - The maximum lead in number of runs maintained by the winner during the game.
  - Total number of innings played in the game.

5. Create histogram plots of the minimum lead maintained by the winners of each game in the season, the average number of outs all the players were involved in during the season and the average number of times the players were able to get on base.

6. Select the group of players that have appeared at bat an above average number of times.  Of this cohort, find the player that was able to get on base the most.  For that player, create a plot of the total games played, singles hit, doubles hit, triples hit, homers hit and walks for each month plotted versus month.  You will find the `resample()` and `apply()` functions very handy here.

7. Most of machine learning involves finding features in data that are somehow statistically connected to other features in data.  One simple way to establish this is using scatter plots and correlation calculations.  Select the group of players in the upper 70th percentile in terms of games played.  From this cohort, use your player summary table to create scatter plots and calculate the correlation coefficient for number of games played by each player versus:
  - Total at bats.
  - Average number of outs the player participated in as a fielder.
  - Average number of times on base.
  - Average RBIs generated by the player.
  - Average number of runs scored by the player.



<br>
<br>
  
