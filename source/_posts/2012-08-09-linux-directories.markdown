---
comments: true
date: 2012-08-09 17:17:00
layout: post
slug: linux-directories
title: Linux directories
wordpress_id: 65
categories:
- exocortex
tags:
- linux
---

Can’t remember where this came from.

**/bin** – Contains the executable programs that are part of the Linux operating system. Many Linux commands, such as cat, cp, ls, more, and tar, are locate in /bin 

**/boot** – Contains the Linux kernel and other files needed by LILO and GRUB boot managers. 

**/dev **– Contains all device files. Linux treats each device as a special file. All such files are located in /dev. 

**/etc **– Contains most system configuration files and the initialisation scripts in /etc/rc.d subdirectory. 

**/home** – Home directory is the parent to the home directories of users. 

**/lib** – Contains library files, including loadable driver modules needed to boot the system. 

**/lost+found** – Directory for lost files. Every disk partition has a lost+found directory. 

**/media **– Directory for mounting files systems on removable media like CD-ROM drives, floppy disks, and Zip drives. 

**/mnt **– A directory for temporarily mounted filesystems. 

**/opt **– Optional software packages copy/install files here. 

**/proc **– A special directory in a virtual filesystem. It contains the information about various aspects of a Linux system. 

**/root **– Home directory of the root user. 

**/sbin **– Contains administrative binary files. Commands such as mount, shutdown, umount, reside here. 

**/srv** – Contains data for services (HTTP, FTP, etc.) offered by the system. 

**/sys** – A special directory that contains information about the devices, as seen by the Linux kernel. 

**/tmp** – Temporary directory which can be used as a scratch directory (storage for temporary files). The contents of this directory are cleared each time the system boots. 

**/usr **– Contains subdirectories for many programs such as the X Window System. 

**/usr/bin** – Contains executable files for many Linux commands. It is not part of the core Linux operating system. 

**/usr/include** – Contains header files for C and C++ programming languages 

**/usr/lib **– Contains libraries for C and C++ programming languages. 

**/usr/local** – Contains local files. It has a si 

milar directories as /usr contains. 

**/usr/sbin **– Contains administrative commands. 

**/usr/share** – Contains files that are shared, like, default configuration files, images, documentation, etc. 

**/usr/src **– Contains the source code for the Linux kernel. 

**/var **– Contains various system files such as log, mail directories, print spool, etc. which tend to change in numbers and size over time. 

**/var/cache** – Storage area for cached data for applications. 

**/var/lib **– Contains information relating to the current state of applications. Programs modify this when they run. 

**/var/lock** – Contains lock files which are checked by applications so that a resource can be used by one application only. 

**/var/log **– Contains log files for differenct applications. 

**/var/mail** – Contains users’ emails. 

**/var/opt **– Contains variable data for packages stored in /opt directory. 

**/var/run **– Contains data describing the system since it was booted. 

**/var/spool** – Contains data that is waiting for some kind of processing. 

**/var/tmp **– Contains temporary files preserved between system reboots.
