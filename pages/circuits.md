---
layout: project
repository_url: https://github.com/ggmessier/frogs
use_math: true
---
# Electronics

This page covers various assorted topics related to hardware and electronics design.

## Printed Circuit Board Design

After being a long time Eagle user, I switched over to [KiCad](https://www.kicad.org/) since it's open source, has an active user and developer community and is just really excellent.  This Phil's Lab [tutorial](https://www.youtube.com/watch?v=aVUqaB0IMh4) is *very* well done and a great place for a new user to start.

The board vendor I use is [Dirty PCBs](https://dirtypcbs.com/store/pcbs/about).  Design rule details:
- The "w/s" spec stands for width/spacing so 6mil (0.16mm) is minimum track width and spacing.  I set this to 0.2mm.
- I set my signal and power trace widths to 0.3mm and 0.5mm, respectively, to be consistent with the tutorial.
- Via size is set to a 0.3mm hole (the minimum allowed) and a via size of 0.7mm (0.3mm hole surrounded by a 0.2mm width copper trace).
- BGA is ball grid array.
- SMD is surface mount device and refers to the pad size of SMD devices.  It's 8mil or 0.2mm.  Most of my SOIC pads seem to default to 0.5mm so this is fine.
- PTH is plated through hole and NPTH is non-plated through hole.

- PTH A/R is aspect ratio.  A value of 8:1 means that a 1.6mm thick board has a PTH of 0.2mm.  This means setting min hole widths to 0.2mm should be pretty safe.

Here's a handy [PCB trace width calculator](https://www.4pcb.com/trace-width-calculator.html).

To make PCB creation cheaper and more efficient, it's often useful to tile or panelize many smaller PCB designs up to the maximum area allowed by your board house (10cm x 10cm in the case of Dirty PCBs).
- Start KiCad's `PCBNew` application in standalone mode.
- Add your different PCB designs using `Append board` from the File pulldown menu.
- Delete/edit your board edges to connect them with tabs and mouse bites as appropriate.


When doing a KiCad gerber file export to DirtyPCBs:
- Check "Use Protel filename extensions".
- Include the copper, paste, silkscreen, mask and edge cut layers.
- Change the edge cut filename extension from `gm1` to `gbr`.
- When creating the drill file, check the option for exporting PTH and NPTH to a single file.





## Circuit Simulation

For the low frequency electronics that I work on, a basic spice simulation works fine.  I learned on [ngspice](https://ngspice.sourceforge.io/) which is still a good choice but I find it's a little easier to use [ltspice](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html) these days since it's a bit more complete.  That said, the [ngspice user manual](https://ngspice.sourceforge.io/docs.html) is still my go-to reference for low level spice syntax.










