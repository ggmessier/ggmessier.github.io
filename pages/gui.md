---
layout: project
repository_url: https://github.com/ggmessier/frogs/tree/master/sw/gui
use_math: true
---
# GUI

This is a simple GUI meant to provide a user interface for a simulation or real time application.  The design goals of the interface are:


- The design follows the model-view-controller (MVC) design convention.
- The view and controller elements (ie. the GUI) run in a web browser.  This allows easy use across a variety of platforms.
- The *model* program is a separate program from the GUI that runs continuously either because it's a long run simulation or is monitoring a physical system in real time.
- The user needs to use the GUI to provide input and view results.  However, the model needs to run in parallel and interact with the user at intervals it determines.

## Background Material

The user interface is implemented using HTML5 which involves developing using a combination of HTML, CSS and Javascript.

HTML is used to place all of the basic elements that will be manipulated by the Javascript code.  A good reference for learning the HTML basics is provided by [W3 Schools](https://www.w3schools.com/html/default.asp) and the Mozilla Developer Network provides a good [HTML reference](https://developer.mozilla.org/en-US/docs/Web/HTML).

## Server Model

This GUI is implemented using [Flask](http://flask.pocoo.org/).  Flask is designed to provide a python based server back-end to a web page interface.  It's design is transaction based where it essentially sits idle and responds to user requests.  This is a problem for interfacing to applications that need to run for long periods of time (ie. simulations) or continuously (ie. real time physical systems).

The solution is to develop an architecture where the Flask server communicates using the [Flask socketIo library](https://flask-socketio.readthedocs.io/en/latest/) with both the GUI and the model.   The GUI Javascript code connects to Flask using [Socket.Io](https://socket.io/) and the python model connects using [python-socketio](https://python-socketio.readthedocs.io/en/latest/).

Since Flask will create two separate instances of itself to serve the GUI and model, it is necessary to create a mechanism for those two instances to share data.  This is achieved using a local sqlite3 database.

Both the GUI and model can submit update and read requests for the shared data stored by the server.  The model is respondible for initializing the shared database and populating it with initial values.  The GUI will update the shared data immediately upon a controller action (ie. user input) and will read the shared data at a certain refresh rate to capture updates made by the model.  The model updates and reads from the shared data at a rate determined by the application.  For example, a long running simulation will limit its interaction with the server to ensure it spends most of its time on computation.  An application monitoring smart home devices may only update when it receives an event trigger.

This version of the software runs on the basic web server that is automatically started by the Flask application.  For deployment on an enterprise scale, a more robust server should be used.

## User Interface

Design objectives:
- Provide an interface to various hardware projects that utilize a [Beaglebone Black](pages/bbb) as a gateway.
- Work well on a small phone screen and a browser running on a regular monitor.

The interface can be divided into *panels* that each correspond to a different functionality.  For example, a smart home interface may have a panel dedicated to light switch control and another one to a backyard weather station.

In a small screen, miniature versions of each panel that display summary information are displayed in a grid pattern.  Each miniature panel can be clicked to bring up the full panel.  On a large screen, the full panels are displayed.

The gui screen consists of one or more *panels*:
- By default, each panel is a minimized.   Summary information is displayed in the minimized panel.
- A panel is maximized by clicking.  When a panel is maximized, the other panels disappear.
