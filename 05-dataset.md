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
The **curl** utility is widely available, and can be used on all the platforms we discuss in this course.
The following example downloads the data set - a single file - from the internet and stores it in the
current directory:

~~~ {.bash}
$ curl -# -O http://neondataskills.org/data/NEON-DS-Landsat-NDVI.zip
~~~
The -O option sends the downloaded file to a local file (rather than to your terminal screen). The -# option 
creates a simple download bar - if you skip this you get some more complex download statistics.

`curl` has lots of useful options. E.g., if you need to restart the above download if you were 
interrupted in the middle, you can use the "-C" option:

~~~ {.bash}
$ curl -# -O -C - http://neondataskills.org/data/NEON-DS-Landsat-NDVI.zip
~~~

This will continue the download from where it was interrupted.

To find out what other options a command like `curl` accepts, we can type `man curl`. `man` is the Unix "manual" command: it prints a description 
of a command and its options, and (if you're lucky) provides a few examples of how to use it.

To navigate through the `man` pages, you may use the up and down arrow keys to move line-by-line, or try the "b" and spacebar keys to skip up 
and down by full page. To search, type "/" followed by some text and "Enter", and "n" to search again.  Quit the `man` pages by typing "q".

~~~ {.bash}
$ man curl
~~~
~~~ {.output}
curl(1)                           Curl Manual                          curl(1)

NAME
       curl - transfer a URL

SYNOPSIS
       curl [options] [URL...]

DESCRIPTION
       curl  is  a tool to transfer data from or to a server, using one of the
       supported protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,  IMAP,
       IMAPS,  LDAP,  LDAPS,  POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS,
       TELNET and TFTP).  The command is designed to work without user  inter‐
       action.

       curl offers a busload of useful tricks like proxy support, user authen‐
       tication, FTP upload, HTTP post, SSL connections, cookies, file  trans‐
       fer  resume,  Metalink,  and more. As you will see below, the number of
       features will make your head spin!

~~~

## Getting data from a USB stick
If the network is slow, you can copy the data set in from a USB stick. 
We went over **cp** in an earlier lesson on "creating things":

> The `cp` command works very much like `mv`, except it copies a file instead of moving it.

On Linux, a USB stick usually mounts under /media/<your_user_name>. You can check by putting in the USB drive and doing

~~~ {.bash}
$ df | tail
~~~

The last line will typically tell you where the USB media has been mounted.

With that info, can you build up a command line to copy the data to your machine? It should look something like

~~~ {.bash}
$ cp /media/<username>/<data_path>/NEON-DS-Landsat-NDVI.zip .
~~~

If you struggle, 

~~~ {.bash}
$ man cp
~~~

could help.

## Verifying that the data is in place
Our earlier lesson also went over the use of `ls`. Can you use it to verify that you have the data set in place on your computer?
