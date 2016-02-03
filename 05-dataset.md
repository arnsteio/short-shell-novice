---
layout: page
title: The Unix Shell
subtitle: Getting the dataset
minutes: 15
---
> ## Learning Objectives {.objectives}
>
> *   Using the command line to get a local copy of the data set
> *   Using the "man" command 

To follow the rest of this workshop you need to get a hold of the data set. We'll use the command line for that. You can either get the data 
from the internet, or via a USB stick the teachers will provide.

## Getting data from the Internet
The **wget** utility is the best option to download files from the internet. 'wget' can handle complex download situations including large file 
downloads, recursive downloads, non-interactive downloads and multiple file downloads. The following example downloads the data set - a single 
file - from the internet and stores in the current directory:

~~~ {.bash}
$ wget secret_data_url
~~~

While downloading it will show a progress bar with the following information:

* percentage of download completion (e.g. 31%)
* Total amount of bytes downloaded so far (e.g. 1,213,592 bytes)
* Current download speed (e.g. 68.2K/s)
* Remaining time to download (e.g. eta 34 seconds)

`wget` has lots of useful options. E.g., if you need to restart the above download if you were interrupted in the middle, you can use the "-c" 
option:

~~~ {.bash}
$ wget -c secret_data_url
~~~

This will continue the download from where it was interrupted.

To find out what other options `wget` accepts, we can type `man wget`. `man` is the Unix "manual" command: it prints a description 
of a command and its options, and (if you're lucky) provides a few examples of how to use it.

To navigate through the `man` pages, you may use the up and down arrow keys to move line-by-line, or try the "b" and spacebar keys to skip up 
and down by full page. Quit the `man` pages by typing "q".

~~~ {.bash}
$ man wget
~~~
~~~ {.output}
WGET(1)                                                       GNU Wget                                                      WGET(1)

NAME
       Wget - The non-interactive network downloader.

SYNOPSIS
       wget [option]... [URL]...

DESCRIPTION
       GNU Wget is a free utility for non-interactive download of files from the Web.  It supports HTTP, HTTPS, and FTP protocols, as well as
       retrieval through HTTP proxies.

       Wget is non-interactive, meaning that it can work in the background, while the user is not logged on.  This allows you to start a 
       retrieval and disconnect from the system, letting Wget finish the work.  By contrast, most of the Web browsers require constant user's 
       presence, which can be a great hindrance when transferring a lot of data.
       ...        ...        ...

OPTIONS
   Option Syntax
       Since Wget uses GNU getopt to process command-line arguments, every option has a long form along with the short one.  Long options are 
       more convenient to remember, but take time to type.  You may freely mix different option styles, or specify options after the 
       command-line arguments.  Thus you may write:

               wget -r --tries=10 http://fly.srk.fer.hr/ -o log
       ...        ...        ...

~~~

## Getting data from a USB stick
We went over **cp** in an earlier lesson on "creating things":

> The `cp` command works very much like `mv`, except it copies a file instead of moving it.

On Linux, a USB stick usually mounts under /media/<your_user_name>. You can check by putting in the USB drive and doing

~~~ {.bash}
$ ls /media
~~~

With that info, can you build up a command line to copy the data to your machine? It should look something like

~~~ {.bash}
$ cp /media/<username>/secret_data_path .
~~~

If you struggle, 

~~~ {.bash}
$ man cp
~~~

could help.

## Verifying that the data is in place
Our earlier lesson also went over the use of `ls`. Can you use it to verify that you have the data set in place on your computer?
