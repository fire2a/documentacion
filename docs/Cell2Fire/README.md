---
layout: default
title: Cell2Fire++
nav_order: 1
has_children: true
has_toc: false
---
# Cell2Fire++
{: .no_toc}
<details closed markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

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
| Dogrib forest, Canada ![](./img/c2fFBP-Example4.png){: width="100%" } | shortest paths propagation ![](./img/c2fFBP-Example1.png){: width="80%" } |
| Shortest paths propagation and ROS intensity ![](./img/c2fFBP-Example2.png){: width="100%" } | Burn-Probability ![](./img/c2fFBP-Example3.png){: width="80%" } |

# Compiling
## Linux
[Make](compile_linux.html)

## Windows
[Using Visual Studio](compile_windows.html)
