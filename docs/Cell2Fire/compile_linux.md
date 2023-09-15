---
layout: default
title: compiling on Linux
nav_order: 1
parent: Cell2Fire++
has_children: false
has_toc: false
---
# Compile on Linux
## debian based
A Cell2Fire++ binary is provided with the release; though to compile it:
```bash
sudo apt install g++ libboost-all-dev libeigen3-dev
cd C2FSB/Cell2FireC
make clean
make 
```  
If it fails, is probably the `makefile` assuming `EIGENDIR = /usr/include/eigen3/`  
Locate where your distribution installs `eigen`, either using the command `nice find / -readable -type d -name eigen3 2>/dev/null` or check your distribution's documentation for `libeigen3-dev` package [^1] [^2]. Edit `makefile` accordingly, then try building again. 

## Rocky Linux (khipu)
```
# boost was installed
# download eigen
git clone git@salsa.debian.org:science-team/eigen3.git

# locate gcc12
find /opt -name "libstdc++*" -print
/opt/gcc/gcc-12.1.0/lib64/libstdc++.so

# append to .bashrc
export LD_LIBRARY_PATH=/opt/gcc/gcc-12.1.0/lib64:$LD_LIBRARY_PATH

# use the modified makefile
EIGENDIR     = /path/to/eigen3/
CC = /opt/gcc/gcc-12.1.0/bin/g++
MPCC = /opt/gcc/gcc-12.1.0/bin/g++
OPENMP = -fopenmp
CFLAGS = -std=c++11 -O3 -I$(EIGENDIR) -fopenmp
```

----

[^1]: https://packages.debian.org/bookworm/all/libeigen3-dev/filelist
[^2]: https://packages.ubuntu.com/search?keywords=libeigen3-dev
