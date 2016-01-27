---
layout: page
title: The Unix Shell
subtitle: Getting the dataset
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> *   Using the command line to get a local copy of the data set
> 

To follow this workshop you need to get a hold of the data set. We'll use the command line for that. You can either get the data from the 
internet, or via a USB stick the teachers will provide.

## Getting data from the Internet
The **wget** utility is the best option to download files from the internet. wget can handle complex download situations including large file 
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

wget has lots of useful options. E.g., if you need to restart the above download if you were interrupted in the middle, you can use the "-c" 
option:

~~~ {.bash}
$ wget -c secret_data_url
~~~

This will continue the download from where it was interrupted.


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

## Verifying that the data is in place
Our earlier lesson also went over the use of `ls`. Can you use it to verify that you have the data set in place on your computer?
