---
layout: default
use_math: true
---
# Baseball Statistics

Looking for a data set to practice data analytics?  Look no further than baseball!  Since 2008, the pitchf/x system has been collecting detailed information on every pitch thrown in every MLB game (speed, ball rotation, movement, pitch type, etc.).  You can download all this data for free along with a bunch of other information on what happened at each at bat.

A good overview of where to find baseball data in general can be found on the [SABR website](https://sabr.org/sabermetrics/data) but the tool I use is Baseball on a Stick (BBOS).


## Baseball on a Stick BBOS Setup

While there are a number of different discussions on the web regarding how to download pitchf/x and other game data, I found the most complete package is [BBOS](https://sourceforge.net/projects/baseballonastic/).  This software downloads both pitchf/x data and retrosheet data and loads it into a MySQL database.

For Linux/Mac people, this package only works on Windows.  My work-around was to run BBOS in a windows virtual machine on my Mac and have it populate a MySQL database running on OSX.  Also, there's a bug in the package that prevents it from working with MySQL 5.7 but the fix is discussed in [this post](https://sourceforge.net/p/baseballonastic/discussion/820145/thread/0f201970/?limit=25#f99d).

## BBOS MySQL Database

- `action`: This table contains coaching interventions and substitutions (mainly pitching changes).

- `atbats`: This is an important table that records the result of every at bat in every game.  The `num` field is an index number for the at bats that starts at 1 for each game.  This is different than `eventNumber` which seems to skip ahead.  Also note that this table would be more accurately named `plateappearances` since the official definition of an "at bat" does not include walks.  However, this table records everything that happens every time a batter appears at the plate.

- `pitches`: A very interesting table which contains the pitchF/X data on every pitch thrown in every MLB game.  While there's a wealth of data here, some important fields are missing (like who the pitcher is).  To link players to pitches, the batter ID, pitcher ID and atbat ID (ie. the `num` field) need to be extracted from the `atbat` table.  The `num` field is then matched up to the `gameAtBatID` field in `pitches`.  An excellent explanation of the pitch fields is [here](https://fastballs.wordpress.com/2007/08/02/glossary-of-the-gameday-pitch-fields/).

- `hitters`: Captures how each hitter performs in each game and series.  All columns that start with a `s_` are series cumulative totals.

There are a number of abbreviations that show up in a few of the tables that you need to understand in order to use the data:

| Abbreviation  | Meaning    |
|:-------------:|:----------:|
| h  | hits |
| bb | walks (base on balls)|
| r | runs |
| go | ground out |
| ao | air out |
| ab | at bat |
| d | double |
| t | triple |
| hbp | hit by pitch |
| sf | sacrificial fly ball |
| sb | stolen bases |
| lob | left on base |
| bf | batters faced |
| er | earned runs |
| so | strike outs | 



## Baseball Stats and Andrew Ng's Machine Learning Lectures

**This section is under construction.**

Stanford has posted the videos of Andrew Ng's excellent machine learning lectures.  This page will describe how to use the BBOS database to try out some of the concepts he discusses.

### Linear Regression

The gradient descent and normal equation discussion utilizes a linear hypothesis function which maps a linear combination of input variables to a single real number output value

$$
h(\theta) = \theta_2 x_2 + \theta_1 x_1 + \theta_0
$$



