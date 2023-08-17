---
layout: default
title: Cell2Fire++
nav_order: 1
has_children: false
has_toc: false
---
# Cell2Fire++

Coming soon: We are working towards unifying the c++ backend.

Meanwhile, current flavors:
- [Scott & Burgan](https://github.com/fire2a/C2FSB)  
- [Kitral](https://github.com/fire2a/C2FK)  
- [FBP](https://github.com/fire2a/C2FFBP)

And the [OG](https://github.com/cell2fire/Cell2Fire/)

# Output examples

## Scott & Burgan
### Previncat's Zone 60 (Catalonian Instance): forest and a simulated fire spread with its corresponding scar and growth propagation tree. 
![Example-Instance_Scar](./img/c2fsb-example-scar.png)
### Risk metrics: Burn Probability (BP), Betweenness Centrality (BC), Downstream Protection Value (DPV), and Growth Propagation Tree (GPT). 
![Example-Risck_Metrics](./img/c2fsb-example-metrics.png)

## Kitral
### El Portillo, simulation with crown fire behavior.
![Example-El Portillo-Crown fire](./img/c2fk-El_portillo.png)

## Canadian Forest Fire Behavior Prediction System

|:-------------|:------------------|
| Dogrib forest Canada ![](./img/c2fFBP-Example4.png) | shortest paths propagation ![](./img/c2fFBP-Example1.png) |
| Shortest paths propagation and ROS intensity ![](./img/c2fFBP-Example2.png) | Burn-Probability ![](./img/c2fFBP-Example3.png) |

# Compiling
## Linux
A Cell2Fire++ binary is provided with the release; anyway to compile it:
```bash
sudo apt install g++ libboost-all-dev libeigen3-dev
cd C2FSB/Cell2FireC
make clean
make 
```  
If it fails, is probably the `makefile` assuming `EIGENDIR = /usr/include/eigen3/`  
Locate where your distribution installs `eigen`, either using the command `nice find / -readable -type d -name eigen3 2>/dev/null` or check your distribution's documentation for `libeigen3-dev` package [^1] [^2]. Edit `makefile` accordingly, then try making again. 

## Windows
[Using Visual Studio](README_VisualStudio.html)

----

[^1]: https://packages.debian.org/bookworm/all/libeigen3-dev/filelist
[^2]: https://packages.ubuntu.com/search?keywords=libeigen3-dev
