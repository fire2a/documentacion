---
layout: default
title: QGIS Fire Analytics Toolbox
nav_order: 1
has_children: true
has_toc : false
---
<i img="max-width: 10%"></i>
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
    - [full guide](./plugin_installation.md)

*Done: fire2a-toolbox icon <img src="./img/bonfire.png"  style="height: 16px"> will appear on the algorithms list of the Processing Toolbox Panel*

(*) : Because it contains compiled c++ binary code -providing the fast and parallel Cell2Fire simulator, however binary code cannot be easily verified hence the plugin is not allowed on the regular repo/store. Nevertheless all our code is open source, its build is "reproducible" by an automated action; all can be audited on [fire2a@github](https://github.com/fire2a)

* **Testers** should instead install by `.zip` file from fire2a-toolbox [releases][toolbox-releases]
* **Developers** should clone both repos, compile, symlink and setup additional python dependencies to contribute

## Test run
Getting or generating a fuel model raster can be challenging (tutorial coming soon), so the simplest way is to:
1. Use the downloader algorithm <img src="./img/downloader.svg"  style="height: 16px"> to get a prepared instance
2. Save an empty project into the downloaded folder (where fuels, elevation and Weather.csv files are)
3. Drag and drop layers from the project home (file Browser Panel) into the Layer Panel
4. Set the same CRS to the layers and project (any in meters suffices)
5. Open the simulator algorithm <img src="./img/forestfire.svg"  style="height: 16px">, select the proper fuelmodel (Canada, Kitral or S&B), select the fuel layer in the fuel dropdown, press run.

Step 2 can be skipped but is more cumbersome to select each layer from a file explorer than to use the dropdown to select between current loaded layers; Also `Weather.csv` is automatically selected.

{: .warning}
Windows users must set `.tif` as their default raster format
![](./img/windows_tif.png)

# Algorithms

__Installation instructions [here]()__  
__QGIS-plugin-repo [link](./plugins.xml)__  

# Usage


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
