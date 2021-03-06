---
layout: default
use_math: true
---

# Baseball Data

It's nice to have a dataset to practice machine learning techniques and the baseball community provides a *huge* amount of data on major league baseball (MLB) games.  In particular, a group of very committed volunteers maintains the [Retrosheet](http://retrosheet.org) project where the outcome of every at-bat in every MLB game going back to 1921!  In addition to Retrosheet, there is even more data that can be downloaded directly from the MLB servers.  In particular, MLB provides access to the pitchf/x system data that contains detailed information on every pitch thrown in the MLB since 2008 (speed, ball rotation, movement, pitch type, etc.).

While the Retrosheet data is more than sufficient for testing whatever machine learning algorithm you're interested in, a good overview of all the data available for download can be found  on the [SABR website](https://sabr.org/sabermetrics/data).

## Baseball on a Stick (BBOS)

**NOTE:** I ran all this code a few years ago now so some of this information may be dated.


While it is possible to download the play-by-play event files for games directly from Retrosheet [here](https://www.retrosheet.org/game.htm), you would spend a fair bit of time loading them into a MySQL database.  The [BBOS](https://sourceforge.net/projects/baseballonastic/) program does this work for you and delivers a MySQL database populated with any year of Retrosheet data you'd like.  This software downloads both pitchf/x data and retrosheet data.

For Linux/Mac people, this package only works on Windows.  My work-around was to run BBOS in a windows virtual machine on my Mac and have it populate a MySQL database running on OSX.  Also, there's a bug in the package that prevents it from working with MySQL 5.7 but the fix is discussed in [this post](https://sourceforge.net/p/baseballonastic/discussion/820145/thread/0f201970/?limit=25#f99d).

Once you've populated your Retrosheet database, the table with all the play-by-play data is ``events``.  The table that links player ID's to their names and positions is ``rosters``.

At this point, you will be working with a combination of SQL queries and a python program to consolidate the data.  The SQL queries will give you a single entry per at-bat in every game and your python program will use this data to populate an offensive timeline for each unique player.  At this point, you will be getting much of your information from the ``event_tx`` field which corresponds to the retrosheet [event field](https://www.retrosheet.org/eventfile.htm).  Using regular expressions is super handy for decyphering these event strings.

