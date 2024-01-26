---
layout: default
title: QGIS Fire Analytics Toolbox
nav_order: 1
has_children: true
has_toc : false
---
# Fire Analytics Toolbox
{: .no_toc}
<details closed markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
## Overview
Our applied fire research as **user friendly graphical GIS tools**:
- *Simulate* large scale wildfires using Cell2Fire++
- Get threat and risk *metrics*
- Use the firebreak location *decision support system*
- *Combine* our algorithms with any other [QGIS] algorithms easily

Without leaving the graphical environment of [QGIS], just by installing our **processing algorithm plugin** *fire2a-toolbox*.

This type of plugins differ from the regular plugins -by being much more than a pop-up dialog- because they follow a data-science-pipeline architecture. 
Clearly delimites: inputs, outputs, algorithms and contexts; achieving seamless integration with all other provided algorithms in the [toolbox], providing 5 ways of being run.

## Usage alternatives
1. Simple as *filling a **[form dialog]*** (checkboxes, dropdowns, file-choosers, etc.); with the minimal inputs being a fuel raster and a weather scenario. 
2. **[Batch of forms]**: Execute sequential runs configuring them in data-sheet-style where each row is one (column-wise displayed) form, *easily experiment parameter sensitivities*.
3. As part of a **[graphical model] workflow**: Drag and drop boxes of parameters and algorithms, conect arrows as input-ouputs between them, into a [custom] *GIS-data-science-pipeline*.
4. From a **command line tool**, run `qgis_process` [cli wrapper] to call any processing algorithm *without QGIS graphical overhead*.
5. **Python script**, working *both* [calling it] from the QGIS [python console] *or* as [standalone code]

## Installing
1. [QGIS] version > 3.28.12 (LTR version is mostly compatible but misses, for example, grouping simulation results; latest version is recommended)
2. fire2a-toolbox installation can *almost* be done straight forward from QGIS **[plugin manager]** *but*:
    - Python dependencies must be manually resolved  
    - fire2a's custom plugin repo/store [link][toolbox-server] must be setup along the default (*)  

3. Done: fire2a-toolbox icon will appear on the algorithms list of the Processing Toolbox Panel

(*) : Because it contains compiled c++ binary code -providing the fast and parallel Cell2Fire simulator, however binary code cannot be easily verified hence the plugin is not allowed on the regular repo/store. Nevertheless all our code is open source, its build is "reproducible" by an automated action; all can be audited on [fire2a@github](https://github.com/fire2a)

* **Testers** should instead install by `.zip` file from fire2a-toolbox [releases][toolbox-releases]
* **Developers** should clone both repos, compile, symlink and setup additional python dependencies to contribute

## First usage
After setting up installation, getting or generating a fuel model raster can be challenging, tutorial coming soon
1. An instances downloader algorithm is provided to getting prepared instances
2. Setup an empty directory with the instances, save a project in it
3. Drag and drop layers from the project home (file Browser Panel) into the Layer Panel

{: .warning}
Windows users must set `.tif` as their default raster format
![](./img/windows_tif.png)

# Algorithms
## Raster knapsack optimization
### Intro
_A proof-of-concept integration of mathematical programming solvers to model and solve optimization problems with GIS entities._

Users can create a new raster layer that selects the most valuable pixels in a raster, according to a capacity constraint defined by another -optional- raster and a fractional ratio.

Several solvers can be used (cbc, glpk, cplex_direct, gurobi, ipopt, NEOS, etc.), thanks to the MIP being modeled and solved through [pyomo](http://www.pyomo.org).

Before running this algorithm, make sure that you have installed the corresponding solvers that you want to use. See [pyomo documentation](https://pyomo.readthedocs.io/en/stable/installation.html#conditional-dependencies) for more  details.

| screenshot |
| --- |
|<img src="img/screenshot.png"  alt='cannot load image' height=400px >|

### Detailed description
By selecting a Values layer and/or a Weights layer, and setting the bound on the total capacity, a layer that maximizes the sum of the values of the selected pixels is created.

The capacity constraint is set up by choosing a ratio (between 0 and 1), that multiplies the sum of all weights (except no-data). Hence 1 selects all pixels that aren't no-data in both layers.

This raster knapsack problem is NP-hard, so a MIP solver engine is used to find "nearly" the optimal solution, because -often- is asymptotically hard to prove the optimal value. So a default gap of 0.5% and a timelimit of 5 minutes cuts off the solver run. The user can experiment with these parameters to trade-off between accuracy, speed and instance size(*). On Windows closing the blank terminal window will abort the run!

By using Pyomo, several MIP solvers can be used: CBC, GLPK, Gurobi, CPLEX or Ipopt; If they're accessible through the system PATH, else the executable file can be selected by the user.

Installation of solvers is up to the user, although the windows version is bundled with CBC unsigned binaries, so their users will face a "Windows protected your PC" warning, please avoid pressing the "Don't run" button, follow the "More info" link, scroll then press "Run anyway".

(*): Complexity can be reduced greatly by rescaling and/or rounding values into integers, or even better coarsing the raster resolution (see gdal translate resolution).

__Installation instructions [here](./plugin_installation.md)__  
__QGIS-plugin-repo [link](./plugins.xml)__  

# Usage
## window dialog
1. Open QGIS Processing Toolbox (the cog icon)
2. Type or navigate to: Fire2a > Raster Knapsack Optimization
3. Select one or two layers, input the capacity ratio
4. Click Run

## command line

## standalone script

## script in QGIS Console

```
from qgis import processing
result = processing.run(
    "Fire2a:Raster Knapsack Optimization",
    {
        "INPUT_ratio": 0.06,
        "INPUT_value": "/path/to/raster.any_supported_extension",
        "INPUT_weight": None,
        "OUTPUT_csv": "TEMPORARY_OUTPUT",
        "OUTPUT_layer": "TEMPORARY_OUTPUT",
        "SOLVER": "cbc: ratioGap=0.001 seconds=300",
        "CUSTOM_OPTIONS_STRING": "",
    },
)
QgsProject.instance().addMapLayer(result['OUTPUT_layer'])
```

# Template
[This repo](https://github.com/fdobad/qgis-processingplugin-template) is a template for QGIS processing toolbox [plugins](https://plugins.qgis.org).

---
[QGIS]: https://qgis.org

[requirements.txt]: https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/requirements.txt 
[requirements.dev.txt]: https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/requirements.dev.txt
[Scott&Burgan-dialog-server]: https://fdobad.github.io/qgis-processingplugin-template/plugins.xml
[Kitral simulator dialog-server]: https://fdobad.github.io/fire2am-kitral/plugins.xml 
[toolbox-repo]: https://www.github.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin

[graphical model]:(https://docs.qgis.org/latest/en/docs/user_manual/processing/modeler.html)
[toolbox]: (https://docs.qgis.org/latest/en/docs/user_manual/processing/toolbox.html)
[form dialog]: (https://docs.qgis.org/latest/en/docs/user_manual/processing/toolbox.html#the-algorithm-dialog)
[Batch of forms]: (https://docs.qgis.org/latest/en/docs/user_manual/processing/batch.html#processing-batch)
[cli wrapper]: (https://docs.qgis.org/latest/en/docs/user_manual/processing/standalone)
[python console]: (https://docs.qgis.org/latest/en/docs/user_manual/plugins/python_console.html#console)
[calling it]: (https://docs.qgis.org/latest/en/docs/user_manual/processing/console.html)
[standalone code]: (https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/script_samples/standalone.py)
[custom]: (https://github.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/tree/main/graphical_models)
[plugin manager]: (https://docs.qgis.org/latest/en/docs/training_manual/qgis_plugins/fetching_plugins.html)

[toolbox-server]: https://fire2a.github.io/fire-analytics-qgis-processing-toolbox-plugin/plugins.xml
[toolbox-releases]: https://github.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/releases
