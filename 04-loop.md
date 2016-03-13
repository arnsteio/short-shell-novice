---
layout: page
title: The Unix Shell
subtitle: Loops
minutes: 15
---
> ## Learning Objectives {.objectives}
>
> *   Write a loop that applies one or more commands separately to each file in a set of files.
> *   Trace the values taken on by a loop variable during execution of the loop.
> *   Explain the difference between a variable's name and its value.
> *   Explain why spaces and some punctuation characters shouldn't be used in file names.
> *   Demonstrate how to see what commands have recently been executed.
> *   Re-run recently executed commands without retyping them.

**Loops** are key to productivity improvements through automation as they allow us to execute 
commands repetitively. Similar to wildcards and tab completion, using loops also reduces the 
amount of typing (and typing mistakes).
Suppose we have several hundred Landsat-derived NDVI raster files named `005_HARV_ndvi_crop.tif`, `037_HARV_ndvi_crop.tif`, and so on.
In this example, we'll use the `NEON-DS-Landsat-NDVI/HARV/2011/NDVI` directory which only has thirteen example files,
but the principles can be applied to many many more files at once.
We would like to modify these files, but also save a version of the original files, naming the copies
`original-005_HARV_ndvi_crop.tif` and `original-037_HARV_ndvi_crop.tif`.
We can't use:

~~~ {.bash}
$ cp *.tif original-*.tif
~~~

because `*.tif` would expand to:

~~~ {.bash}
005_HARV_ndvi_crop.tif  133_HARV_ndvi_crop.tif  213_HARV_ndvi_crop.tif  261_HARV_ndvi_crop.tif 
037_HARV_ndvi_crop.tif  181_HARV_ndvi_crop.tif  229_HARV_ndvi_crop.tif  277_HARV_ndvi_crop.tif
085_HARV_ndvi_crop.tif  197_HARV_ndvi_crop.tif  245_HARV_ndvi_crop.tif  293_HARV_ndvi_crop.tif
309_HARV_ndvi_crop.tif
~~~

And you cannot copy several files into `original-*.tif`

This wouldn't back up our files, instead we get an error:

~~~ {.error}
cp: target `original-*.tif' is not a directory
~~~

This a problem arises when `cp` receives more than two inputs. When this happens, it
expects the last input to be a directory where it can copy all the files it was passed.
Since there is no directory named `original-*.tif` in the `NEON-DS-Landsat-NDVI/HARV/2011/NDVI` directory we get an
error.

Instead, we can use a **loop**
to do some operation once for each thing in a list.
Here's a simple example that displays the first three lines of each file in our previous `InSitu_Data` directory:

~~~ {.bash}
$ cd ~/Documents/data/NEON-DS-Landsat-NDVI/HARV/2011/NDVI
$ for filename in  005_HARV_ndvi_crop.tif 037_HARV_ndvi_crop.tif 085_HARV_ndvi_crop.tif
> do
>    echo "File to process: $filename"
> done
~~~
~~~ {.output}
File to process: 005_HARV_ndvi_crop.tif
File to process: 037_HARV_ndvi_crop.tif
File to process: 085_HARV_ndvi_crop.tif
~~~

When the shell sees the keyword `for`,
it knows it is supposed to repeat a command (or group of commands) once for each thing in a list.
In this case, the list is the three filenames.
Each time through the loop,
the name of the thing currently being operated on is assigned to
the **variable** called `filename`.
Inside the loop,
we get the variable's value by putting `$` in front of it:
`$filename` is `005_HARV_ndvi_crop.tif` the first time through the loop,
`037_HARV_ndvi_crop.tif` the second, and so on. In this case, the command prints (echoes) the filename to process but we could call a R program and run it over each filename.

By using the dollar sign we are telling the shell interpreter to treat
`filename` as a variable name and substitute its value on its place,
but not as some text or external command. When using variables it is also 
possible to put the names into curly braces to clearly delimit the variable
name: `$filename` is equivalent to `${filename}`, but is different from
`${file}name`. You may find this notation in other people's programs.

> ## Follow the Prompt {.callout}
>
> The shell prompt changes from `$` to `>` and back again as we were
> typing in our loop. The second prompt, `>`, is different to remind
> us that we haven't finished typing a complete command yet. A semicolon, `;`, 
> can be used to separate two commands written on a single line.

We have called the variable in this loop `filename`
in order to make its purpose clearer to human readers.
The shell itself doesn't care what the variable is called;
if we wrote this loop as:

~~~ {.bash}
for x in 005_HARV_ndvi_crop.tif 037_HARV_ndvi_crop.tif 085_HARV_ndvi_crop.tif
do
    echo "File to process: $x"
done
~~~

or:

~~~ {.bash}
for temperature in 005_HARV_ndvi_crop.tif 037_HARV_ndvi_crop.tif 085_HARV_ndvi_crop.tif
do
    echo "File to process: $temperature"
done
~~~

it would work exactly the same way.
*Don't do this.*
Programs are only useful if people can understand them,
so meaningless names (like `x`) or misleading names (like `temperature`)
increase the odds that the program won't do what its readers think it does.

Here's a slightly more complicated loop:

~~~ {.bash}
for filename in *.tif

do 
    echo "File to process: $filename"    
    gdalinfo $filename | tail -5
done
~~~

The shell starts by expanding `*.tif` to create the list of files it will process.
The **loop body**
then executes three commands for each of those files.
The first, `echo`, just prints its command-line parameters to standard output.
For example:

~~~ {.bash}
$ echo hello there
~~~

prints:

~~~ {.output}
hello there
~~~

In this case,
since the shell expands `$filename` to be the name of a file,
`echo "File to process: $filename"` just prints the name of the file after "File to process:".
Note that we can't write this as:

~~~ {.bash}
for filename in *.tif
do
    $filename
    gdalinfo $filename | tail -5
done
~~~

because then the first time through the loop,
when `$filename` expanded to `005_HARV_ndvi_crop.tif`, the shell would try to run `005_HARV_ndvi_crop.tif` as a program.
Finally,
the `gdalinfo` command returns information about the raster data and `tail` combination selects last 5 lines from whatever file is being processed.


> ## Spaces in Names {.callout}
> 
> Filename expansion in loops is another reason you should not use spaces in filenames.
> Suppose our data files are named:
> 
> ~~~
> 005_HARV_ndvi_crop.tif  
> 005_HARV_ndvi_crop extraInfo.tif
> 005_HARV_ndvi_crop_data_desc.tif
> ~~~
> 
> If we try to process them using:
> 
> ~~~
> for filename in *.tif
> do
>     gdalinfo $filename | tail -5
> done
> ~~~
> 
> then most bash shell will expand `*.tif` to create:
> 
> ~~~
> 005_HARV_ndvi_crop.tif 005_HARV_ndvi_crop extraInfo.tif 005_HARV_ndvi_crop_data_desc.tif 
> ~~~
> 
>
> That's a problem: `gdalinfo` can't read a file called `005_HARV_ndvi_crop`
> because it doesn't exist,
> and won't be asked to read the file `005_HARV_ndvi_crop extraInfo.tif`.
> 
> We can make our script a little bit more robust
> by **quoting** our use of the variable:
> 
> ~~~
> for filename in *.tif
> do
>     gdalinfo "$filename" | tail -5
> done
> ~~~
>
> but it's simpler just to avoid using spaces (or other special characters) in filenames.

Going back to our original file copying problem,
we can solve it using this loop:

~~~ {.bash}
for filename in *.tif
do
    cp "$filename" original-"$filename"
done
~~~

This loop runs the `cp` command once for each filename.
The first time,
when `$filename` expands to `005_HARV_ndvi_crop.tif`,
the shell executes:

~~~ {.bash}
cp 005_HARV_ndvi_crop.tif original-005_HARV_ndvi_crop.tif
~~~

The second time, the command is:

~~~ {.bash}
cp 037_HARV_ndvi_crop.tif original-037_HARV_ndvi_crop.tif
~~~

> ## Measure Twice, Run Once {.callout}
> 
> A loop is a way to do many things at once --- or to make many mistakes at
> once if it does the wrong thing. One way to check what a loop *would* do
> is to echo the commands it would run instead of actually running them.
> For example, we could write our file copying loop like this:
> 
> ~~~
> for filename in *.tif
> do
>     echo cp $filename original-$filename
> done
> ~~~
> 
> Instead of running `cp`, this loop runs `echo`, which prints out:
> 
> ~~~
> cp 005_HARV_ndvi_crop.tif original-005_HARV_ndvi_crop.tif
> cp 037_HARV_ndvi_crop.tif original-037_HARV_ndvi_crop.tif
> .
> .
> .
> ~~~
> 
> *without* actually running those commands. We can then use up-arrow to
> redisplay the loop, back-arrow to get to the word `echo`, delete it, and
> then press "enter" to run the loop with the actual `cp` commands. This
> isn't foolproof, but it's a handy way to see what's going to happen when
> you're still learning how loops work.

> ## Those Who Know History Can Choose to Repeat It {.callout}
> 
> Another way to repeat previous work is to use the `history` command to
> get a list of the last few hundred commands that have been executed, and
> then to use `!123` (where "123" is replaced by the command number) to
> repeat one of those commands. For example, if Jessica types this:
> 
> ~~~
> $ history | tail -5
>   456  ls -l *.txt
>   457  rm stats-NENE01729B.txt.txt
>   458  for filename in *.tif; do     cp "$filename" original-"$filename"; done
>   459  ls -l original-*.tif
>   460  history
> ~~~
> 
> then she can re-run `ls -l *.txt` simply by typing
> `!456`.

> ## Variables in Loops {.challenge}
> 
> Suppose that `ls` initially displays:
> 
> ~~~
> rh.grib    temperature.grib   vo.grib
> ~~~
> 
> What is the output of:
> 
> ~~~
> for datafile in *.grib
> do
>     ls *.grib
> done
> ~~~
>
> Now, what is the output of:
>
> ~~~
> for datafile in *.grib
> do
>	ls $datafile
> done
> ~~~
>
> Why do these two loops give you different outputs?

> ## Saving to a File in a Loop - Part One {.challenge}
>
> In the same directory, what is the effect of this loop?
> 
> ~~~
> for file in *.grib
> do
>     echo $file
>     cat $file > bigfile.grib
> done
> ~~~
> 
> 1.  Prints `rh.grib`, `temperature.grib`, and `vo.grib`, and the content from `vo.grib` will be saved to a file called `bigfile.grib`.
> 2.  Prints `rh.grib`, `temperature.grib`, and `vo.grib`, and the text from all three files would be 
>     concatenated and saved to a file called `bigfile.grib`.
> 3.  Prints `rh.grib`, `temperature.grib`, `vo.grib`, and
>     `bigfile.dat`, and the text from `vo.grib` will be saved to a file called `bigfile.grib`.
> 4.  None of the above.

> ## Saving to a File in a Loop - Part Two {.challenge}
>
> In another directory, where `ls` returns:
>
> ~~~
> rh.grib    temperature.grib   vo.grib   z.txt
> ~~~
> 
> What would be the output of the following loop?
>
> ~~~
> for datafile in *.grib
> do
>     cat $datafile >> file.grib
> done
> ~~~
>
> 1.  All of the content from `rh.grib`, `temperature.grib` and `vo.grib` would be 
>     concatenated and saved to a file called `file.grib`.
> 2.  The content from `vo.grib` will be saved to a file called `file.grib`.
> 3.  All of the content from `rh.grib`, `temperature.grib`, `vo.grib` and `z.txt`
>     would be concatenated and saved to a file called `file.grib`.
> 4.  All of the content from `rh.grib`, `temperature.grib` and `vo.grib` would be printed
>     to the screen and saved to a file called `file.grib`

> ## Doing a Dry Run {.challenge}
>
> Suppose we want to preview the commands the following loop will execute
> without actually running those commands:
>
> ~~~ {.bash}
> for file in *.grib
> do
>   analyze $file > analyzed-$file
> done
> ~~~
>
> What is the difference between the two loops below, and which one would we
> want to run?
>
> ~~~ {.bash}
> # Version 1
> for file in *.grib
> do
>   echo analyze $file > analyzed-$file
> done
> ~~~
>
> ~~~ {.bash}
> # Version 2
> for file in *.grib
> do
>   echo "analyze $file > analyzed-$file"
> done
> ~~~

> ## Nested Loops and Command-Line Expressions {.challenge}
>
> The `expr` does simple arithmetic using command-line parameters:
> 
> ~~~
> $ expr 3 + 5
> 8
> $ expr 30 / 5 - 2
> 4
> ~~~
> 
> Given this, what is the output of:
> 
> ~~~
> for left in 2 3
> do
>     for right in $left
>     do
>         expr $left + $right
>     done
> done
> ~~~

