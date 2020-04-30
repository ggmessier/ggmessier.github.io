---
layout: project
repository_url: https://github.com/ggmessier/data-analytics
use_math: true
---
# New Student Orientation

This page will provide a series of exercises meant to bring new research students up to speed on some of the data tools I use in my research group.  While you will likely end up using different data for your research project, these pages utilize publically available baseball data downloaded from the amazing [Retrosheet](http://www.retrosheet.org) website. I used the Baseball on a Stick code to create my baseball database, as I describe [here](data-baseball). 

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

While it is possible to interact with a MySQL server using a terminal program, as described in the tutorial, it is more common to interact with a database using a database browser or studio tool.  The program we will use is the community edition of the multi-platform [DBeaver](https://dbeaver.io) tool.  Documentation for how to use DBeaver is found [here](https://github.com/dbeaver/dbeaver/wiki).  You can focus on the "General User Guide" sections only.

### SQL Exercises

- Using the information from Dr. Messier, create a connection to the MySQL server within DBeaver.
- Open and browse the `Events` and `Rosters` tables.
- Use SQL queries to do the following:

1. Determine how many games have been played in total during the season?
1. Determine how many home games were played by the New York Yankees?
1. Determine how many away games were played by the Toronto Blue Jays?
1. Determine what player has hit the most RBI's? 
1. Create a table of all hits generated in each game.  The table columns should be `Time`, `FirstName`, `LastName`, `PlayerTeam`.  This will require you to join the tables together.  [This](https://www.javatpoint.com/mysql-join) is a good summary of MySQL table join operations.
1. Determine the total number of hits scored in the 2018 season.
1. Determine the total number of hits scored in the 2018 season by players with last name ending in "ez".


To solve the last exercise, you'll need to use the regular expression functionality built into MySQL.  Regular expressions are a very powerful string parsing language that is available in a variety of programming languages (including python).  There are a vast number of regular expression tutorials on the web but a very good and comprehensive tutorial can be found [here](https://www.princeton.edu/~mlovett/reference/Regular-Expressions.pdf).  This document is quite long so here's a [more succinct summary](https://cs.lmu.edu/~ray/notes/regex/) that I've found helpful.  There's also a useful [online regex testing engine](https://regex101.com/) for experimenting with your own test strings as you learn the syntax.



