---
layout: page
title: The Unix Shell
subtitle: Introducing the Shell
minutes: 5
---
> ## Learning Objectives {.objectives}
>
> *   Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs.
> *   Explain when and why command-line interfaces should be used instead of graphical interfaces.

At a high level, computers do four things:

-   run programs
-   store data
-   communicate with each other
-   interact with us

They can do the last of these in many different ways,
including direct brain-computer links and speech interfaces.
Since these are still in their infancy,
most of us use windows, icons, mice, and pointers.
These technologies didn't become widespread until the 1980s,
but their roots go back to Doug Engelbart's work in the 1960s,
which you can see in what has been called
"[The Mother of All Demos](http://www.youtube.com/watch?v=a11JDLBXtPQ)".

Going back even further,
the only way to interact with early computers was to rewire them.
But in between,
from the 1950s to the 1980s,
most people used line printers.
These devices only allowed input and output of the letters, numbers, and punctuation found on a standard keyboard,
so programming languages and interfaces had to be designed around that constraint.

This kind of interface is called a
**command-line interface**, or CLI,
to distinguish it from a
**graphical user interface**, or GUI,
which most people now use.
The heart of a CLI is a **read-evaluate-print loop**, or REPL:
when the user types a command and then presses the enter (or return) key,
the computer reads it,
executes it,
and prints its output.
The user then types another command,
and so on until the user logs off.

This description makes it sound as though the user sends commands directly to the computer,
and the computer sends output directly to the user.
In fact,
there is usually a program in between called a
**command shell**.
What the user types goes into the shell,
which then figures out what commands to run and orders the computer to execute them. Note, the shell is called *the shell* because it encloses the operating system in order to hide some of its complexity and make it simpler to interact with.

A shell is a program like any other.
What's special about it is that its job is to run other programs
rather than to do calculations itself.
The most popular Unix shell is Bash,
the Bourne Again SHell
(so-called because it's derived from a shell written by Stephen Bourne --- this
is what passes for wit among programmers).
Bash is the default shell on most modern implementations of Unix
and in most packages that provide Unix-like tools for Windows.

Using Bash or any other shell
sometimes feels more like programming than like using a mouse.
Commands are terse (often only a couple of characters long),
their names are frequently cryptic,
and their output is lines of text rather than something visual like a graph.
On the other hand,
the shell allows us to combine existing tools in powerful ways with only a few keystrokes
and to set up pipelines to handle large volumes of data automatically thus improving productivity and reproducibility.
In addition, the command line is often the easiest way to interact with remote machines and supercomputers.
Familiarity with the shell is near essential to run a variety of specialised tools and resources including high-performance computing systems. As clusters and cloud computing systems become more popular for scientific data crunching,
being able to interact with them is becoming a necessary skill. We can build on the command-line skills covered here to tackle a wide range of scientific questions and computational challenges.

## Jessica's dissertation: Starting Point

Jessica is putting together her dissertation proposal as a part of her PHD program in ecology at University of Boulder, CO. She is interested in exploring some of her field sites to understand how phenology of vegetation (greening in the spring summer and senescence in the winter, varies across multiple sites and through time. Her PhD advisor has given her some data for a few sites which have very different vegetation communities including Harvard Forest (Massachusetts) and San Joaquin Experimental Range (California). The data include:

1. Vegetation greenness (NDVI) derived from the Landsat Satellite (30 meter resolution) for both sites for 2 years derived from the landsat sensor in a raster format. 
2. Some high resolution images of the sites. 
3. A canopy height model showing tree height 
4. A DEM (digital elevation model) showing topography. 
5. Site temperature, PAR (Photosynthetic active radiation), Soil temperature, Precipitation and daylength for each day over those two years

Jessica has done some of the things above using her favorite open source GIS tool - QGIS. However that workflow makes it difficult to process and look at multiple years worth of data. She wants to create an efficient reproducible workflow that she can use as she collects data for more sites and years over time to support her dissertation work. She has never opened shapefiles and rasters in a non-gui environment. She also understands what a raster is but doesn’t know where the ndvi data come from.

Jessica would like to create the following outputs to better understand her project:

- Plots of temperature, precipitation, PAR and daylength over the 2 year time period (metrics which related to the greening and browning of plants) compared to NDVI (greenness).
- Basemaps of her site showing
	- The location of the tower that measured the above variables and imagery showing what the site look like. 
	- Tree height
	- Topography
- A time series animation of NDVI for both sites that she can post on her blog.
