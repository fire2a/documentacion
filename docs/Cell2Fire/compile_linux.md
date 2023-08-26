---
layout: default
title: compiling on Linux
nav_order: 1
parent: Cell2Fire++
has_children: false
has_toc: false
---
# Compile on Linux
A Cell2Fire++ binary is provided with the release; though to compile it:
```bash
sudo apt install g++ libboost-all-dev libeigen3-dev
cd C2FSB/Cell2FireC
make clean
make 
```  
If it fails, is probably the `makefile` assuming `EIGENDIR = /usr/include/eigen3/`  
Locate where your distribution installs `eigen`, either using the command `nice find / -readable -type d -name eigen3 2>/dev/null` or check your distribution's documentation for `libeigen3-dev` package [^1] [^2]. Edit `makefile` accordingly, then try building again. 

----

[^1]: https://packages.debian.org/bookworm/all/libeigen3-dev/filelist
[^2]: https://packages.ubuntu.com/search?keywords=libeigen3-dev
