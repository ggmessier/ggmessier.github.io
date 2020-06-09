---
layout: default
---

## Teaching Experience

### Undergraduate
ENEL 573 – Computer Networks (Fall 2017, Fall 2016, Fall 2015, Fall 2014, Fall 2013, Winter 2013)<br>
ENEL 300 – Electrical and Computer Engineering Design (Winter 2013)<br>
ENEL 571 – Digital Communications (Winter 2011, Fall 2009, Winter 2009, Winter 2008, Fall 2006, Fall 2005)<br>
ENEL 419 – Probability and Random Variables for Electrical Engineers (Fall 2010, Fall 2009, Fall 2008)<br>
ENEL 471 – Analog Communications, Lab Instructor (Fall 2007)<br>
ENCM 493 – Software Development for Computer Engineers (Winter 2007, Winter 2006, Winter 2005)<br>

### Graduate
ENEL 649 – Random Variables and Stochastic Processes (Fall 2017, Fall 2016, Fall 2010, Winter 2010, Fall 2008, Fall 2007, Fall 2006, Fall 2005)<br>
ENEL 675 – Digital Communications (Winter 2015, Spring 2014, Winter 2007, Winter 2006, Winter 2005, Fall 2012)<br>


## Projects, Labs, etc.

### Simulating Networks

For my ENEL 573 class, I use the [GNS3](https://gns3.com) network simulation software.  Like other simulation packages, this tool allows us to create a network using a graphical interface.  However, the really cool part of GNS3 is that we can create network nodes that boot up as individual linux machines running inside [QEMU](https://www.qemu.org) when the simulation starts.  Plus, we can run the full version of [wireshark](https://www.wireshark.org) to monitor the packets that run between nodes in the simulation.  Since these nodes are running full linux operating systems, they have all the same header information that we would see when monitoring packets in a live network.

GNS3 is designed to run a variety of operating systems within a variety of virtual machine engines.  I like QEMU and linux since both are open source and free for students.  Also, working in a linux terminal interface is a good learning experience since many network devices run *nix style operating systems.

To use linux in GNS3 it's necessary to create a QEMU compatible linux image that can be loaded with different linux packages and the custom programs/files that I use for teaching. 