---
layout: default
title: Algorithms Library
nav_order: 3
has_toc: false
---
{: .warning}
CLI Python code; Check the graphical user friendly version: [fire2a toolbox](docs/qgis-toolbox/README.html)
# fire2a-lib
{: .no_toc}
<details closed markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This library is python package composed of our novel fire related algorithms, common utilities and tools for GIS, optimization, clustering, etc.

Some use cases:

* Want to look at DownStream Protection Value implementation code?
* I forgot again, how to load a .tif raster into a numpy array + a properties dictionary?

Developers & academic researchers are welcome to contribute!

* [Repository]  
* [API Documentation]

## Quickstart
We strongly recommend installing [QGIS] before usage, although not all modules depend on it. 
```bash
$ pip install git+https://github.com/fire2a/fire2a-lib.git
$ ipython
In [1]: from fire2a.<press-tab-to-continue>
```
Algo check the [qgis-cookbook] and [Repository] guides.

---
[QGIS]: https://qgis.org
[Repository]: https://github.com/fire2a/fire2a-lib/
[API Documentation]: https://fire2a.github.io/fire2a-lib/src/index.html
[dialog-plugin]: qgis-dialog/README.html
[processing-toolbox-plugin]: qgis-toolbox/README.html
[qgis-cookbook]: qgis-cookbook/README.html
