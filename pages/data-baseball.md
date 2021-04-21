---
layout: default
use_math: true
---
# Baseball!

The individuals in our shared dataset are actually baseball players.  The game of baseball and statistics go hand in hand and the excellent [Retrosheet](https://www.retrosheet.org/) website has the sequence of events that have occurred for every at-bat in every major league baseball game dating all the way back to 1916!  This is obviously a wonderful and very rich public domain dataset for playing around with data analytics.


## Introduction to the Game

If you're not familiar with baseball, here are some of the many resources that describe the basics of the game:
- [Wiki-How Baseball Tutorial](https://www.wikihow.com/Play-Baseball)
- [Quick Baseball Guide](https://www.tutorialspoint.com/baseball/baseball_quick_guide.htm)
- [The Rules of Baseball - EXPLAINED! (Video)](https://www.youtube.com/watch?v=skOsApsF0jQ)
- [Baseball Explained in 5 Minutes (Video)](https://www.youtube.com/watch?v=I8VGW0C_GO4)


## Fantasy Baseball

Many of our applications involve using data science to detect individuals with unusual or exceptional characteristics.  There are actually a large number of baseball players that move through the major leagues every year.  Some play for a long time and some only for a very short time.  While they are all very gifted athletes, there are still a smaller group that stand out as "exceptional".

To indentify these individuals, we use fantasy baseball scoring metrics to identify a sub-population of players that have a significant positive impact on their teams.  We then use various data features to predict which players will fall into that population.

Due to its popularity, we base our analysis on [Yahoo Sports](https://baseball.fantasysports.yahoo.com) fantasy baseball platform.  The offensive impact of a batter is evaluated by assigning points as follows:
- Singles (1B): 2.6
- Doubles (2B): 5.2
- Triples (3B): 7.8
- Home Runs (HR): 10.4
- Runs (R): 1.9
- Runs Batted In (RBI): 1.9
- Bases on Balls (BB): 2.6
- Stolen Bases (SB): 4.2
- Hit by Pitch (HBP): 2.6


## Data Transformation

To disguise Retrosheet data as health and emergency service patient data, we use the following mapping:

- **Adverse Outcome:** When a player's Yahoo fantasty baseball points score crosses the threshold of the top 10% of players.
- **Major Event:** Hitting a home run.  This is positively correlated with an "Adverse Outcome" since players with high fantasy baseball scores hit a lot of home runs.
- **Stay:** Being on the starting player roster for a game.  This is also positively correlated with an "Adverse Outcome" since players that play a lot accumulate a lot of points.  However, it's not quite as good as hitting a home run.
- *Referral:** Being drafted, traded or a free agent.  This is negatively correlated with an "Adverse Outcome" since less skilled players tend to be traded more than star players.  These events can also signal a player who is reaching the end of their career.

<br>
<br>