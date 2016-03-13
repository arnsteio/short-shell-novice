---
layout: page
title: The Unix Shell
subtitle: Setup for the rest of the workshop
minutes: 15
---
> ## Learning Objectives {.objectives}
>
> *   Run a shell script from the command line.
> *   Check all the necessary R packages are installed on your laptop

In the previous lessons, we have learnt to list, create, inspect, rename and delete files and directories from the command line in a shell window. In a very similar way, we can start R (or rstudio) from the command line.

Let's open a shell window:

~~~ {.bash}
$ R
~~~
~~~ {.output}
R version 3.2.3 (2015-12-10) -- "Wooden Christmas-Tree"
Copyright (C) 2015 The R Foundation for Statistical Computing
Platform: x86_64-redhat-linux-gnu (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

[Previously saved workspace restored]

> 
~~~


If you start rstudio instead, a new window will pop-up:

~~~ {.bash}
$ rstudio
~~~

![Rstudio in action](fig/rstudio.png)

Remark: rstudio can usually be started by clicking on the Rstudio icon from your menu (or Desktop if you have a shortcut).

If any of these two commands (R and rstudio) don't work (command not found), check you have followed the [setup instructions](http://neondataskills.org/workshop-event/NEON-Data-Carpentry-Spatio-Temporal-Oslo-03-15#R-windows) and ask for help!

Now you are ready to check all the necessary R packages are installed on your laptop.
From R or rstudio console:

~~~ {.bash}
> library(raster)
~~~
~~~ {.output}
Loading required package: sp
~~~
~~~ {.bash}
> library(rgdal)
~~~
~~~ {.output}
rgdal: version: 1.1-3, (SVN revision 594)
 Geospatial Data Abstraction Library extensions to R successfully loaded
 Loaded GDAL runtime: GDAL 1.10.1, released 2013/08/26
 Path to GDAL shared files: /usr/share/gdal/1.10
 Loaded PROJ.4 runtime: Rel. 4.8.0, 6 March 2012, [PJ_VERSION: 480]
 Path to PROJ.4 shared files: (autodetected)
 Linking to sp version: 1.2-2 
~~~
~~~ {.bash}
> library(rasterVis)
~~~
~~~ {.output}
Loading required package: lattice
Loading required package: latticeExtra
Loading required package: RColorBrewer
~~~
~~~ {.bash}
> library(ggplot2)
~~~
~~~ {.output}

Attaching package: ‘ggplot2’

The following object is masked from ‘package:latticeExtra’:

    layer

~~~
~~~ {.bash}
> library(sp)
> library(rgeos)
~~~
~~~ {.output}
rgeos version: 0.3-17, (SVN revision 520)
 GEOS runtime version: 3.4.2-CAPI-1.8.2 r3921 
 Linking to sp version: 1.2-2 
 Polygon checking: TRUE 

> 

~~~

Please note that you may get slightly different outputs but no errors should occur. In particular if you get (for any of the required packages):

~~~ {.error}
Error in library(rgdal) : there is no package called ‘rgdal’
~~~

It means that the above package (here `rgdal`) is not installed on your system.

Tell us if there is anything wrong! Our helpers would be happy to help you to install the necessary R packages on your laptop!

