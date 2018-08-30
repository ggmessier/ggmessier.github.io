---
layout: default
use_math: true
---

# Machine Learning Software Development

Our machine learning work is done using numerical python ([NumPy](http://www.numpy.org/)) attached to a mySQL database front-end.  The machine learning algorithms are implemented and tested using NumPy and the raw data is contained in the database.  If you're a student in my research lab, it's assumed you're doing your work on an Ubuntu linux PC.

## MySQL

[MySQL](https://www.mysql.com/) is an open source [relational database](https://en.wikipedia.org/wiki/Relational_database) maintained by Oracle that implements its interface using the standardized structured query language (SQL).  MySQL utilizes a client/server model where the server is responsible for the database and the client accesses data from the database by sending SQL queries to the server.  While there are an uncountable number of MySQL references on the web, a good place to start is [this tutorial](https://downloads.mysql.com/docs/mysql-tutorial-excerpt-5.5-en.pdf).

The python client we utilize is [pymysql](https://github.com/PyMySQL/PyMySQL) which comes standard both with most Linux distributions and Mac Ports.  This allows a python program to make queries to a MySQL server and load database data directly into python data structures (lists, arrays, etc.).

If you're just learning SQL queries, the [MySQL Workbench](https://dev.mysql.com/downloads/workbench/) program is a nice tool that allows you to connect to a MySQL server, submit SQL queries and see the results in a table format.  This is a really good way to test to make sure your queries work before implementing them in python. 

## Python

Your python programs should make use of the numerical python (NumPy), scientific python (SciPy) and matplotlib libraries.  All of these can be installed using Mac ports or your linux distribution (ie. using ``apt-get``).  It's useful to do your development within [Eclipse](http://www.eclipse.org) using the [PyDev](http://www.pydev.org/) development extension.  In particular, PyDev allows you to use a debugger within the eclipse environment.

## Working with Raw Data

Often when working with raw data, it is necessary to search for text strings that contain certain characters or patterns.  For example, when working with Retrosheet baseball data, any event string that starts with an "S" represents a single hit, any string that contains the characters "-H" one or more times represents one or more runs reaching home, etc.  When performing text string analysis and pattern matching, both python and SQL queries allow for the use of the very powerful *regular expression* text parsing language.  There are a vast number of regular expression tutorials on the web but a very good and comprehensive tutorial can be found [here](https://www.princeton.edu/~mlovett/reference/Regular-Expressions.pdf).
