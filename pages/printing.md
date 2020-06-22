---
layout: project
repository_url: https://github.com/ggmessier/frogs/tree/master/mech
use_math: true
---

# 3D Printing 

### Overview
- I have a [Prusa](http://prusa3d.com) i3 MK2S printer.  I chose the build your own option to save a bit of money and get to know the printer a bit better.  It was worthwhile and the user comments in the online build manual were invaluable.
- My CAD package of choice is [FreeCAD](https://www.freecadweb.org).
- The slicer program I use is [PrusaSlicer](https://www.prusa3d.com/prusaslicer/).

### Tutorial Resources

- Like all CAD packages, FreeCAD has a bit of a learning curve.  My go-to resource is this [excellent tutorial](https://wiki.freecadweb.org/Basic_Part_Design_Tutorial_017) which covers everything I need to create a basic part.
- Engraving or creating raised text on a design is very common.  The standard tutorial is [here](https://wiki.freecadweb.org/Draft_ShapeString_tutorial) which I found a bit complex.  However, at the end of the tutorial, there is a reference to [this thread](https://forum.freecadweb.org/viewtopic.php?f=3&t=36623) which talks about binding a 2D draft object to a surface.  Go with the flat face option and when extruding and choose reference rather than one of the copy options.


### Printing
1. Once you've created your design in FreeCAD, select the Body in the tree view that represents the entire part.
1. Using the `File` pulldown menu, select `Export..` as an STL file.
1. Import the STL file into the slicer program.  Adjust the desired print resolution and fill settings.
1. Export from the slicer as a GCODE file and copy that file to the printer's SD card.





