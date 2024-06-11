---
layout: default
title: Algorithms Library
nav_order: 3
has_toc: false
---
{: .warning}
CLI Python code; Check the graphical user friendly version: [fire2a toolbox](/docs/qgis-toolbox/README.html)
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

* Want to look/use/adapt DownStream Protection Value implementation code?
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
[tl;dr developer here](/docs/Cell2Fire/README.html#unix-overview)

## Developer guide
A tree of principal components:
```bash
~
├── C2F-W
│   ├── Cell2Fire
│   │   ├── Cell2Fire
│   │   ├── Cell2Fire.exe
│   │   ├── Cell2Fire.Linux.x86_64
│   │   └── Cell2Fire.Darwin.arm64
│   └── data
│       ├── CanadianFBP
│       ├── Kitral
│       └── ScottAndBurgan
├── fire2a-lib
│   ├── pyproject.toml
│   ├── requirements.dev.txt
│   ├── requirements.doc.txt
│   ├── requirements.txt
│   ├── src
│   │   ├── fire2a
│   │   │   ├── __init__.py
│   │   │   ├── raster.py
│   │   │   ├── ...
│   │   │   └── utils.py
│   │   └── fire2a-tutorials
│   │       ├── __init__.py
│   │       └── template.py
│   └── tests
│       ├── assets
│       └── test_utils.py
└── fire-toolbox
    └── fireanalyticstoolbox
        ├── metadata.txt
        ├── __init__.py
        ├── fireanalyticstoolbox.py
        ├── fireanalyticstoolbox_provider.py
        ├── fireanalyticstoolbox_algorithm.py
        ├── algorithm_...py
        ├── requirements.txt
        ├── fire2a -> ~/fire2a-lib/src/fire2a (versión release)
        └── simulator
            ├── C2F -> ~/C2F-W
            ├── c2fqprocess.py
            ├── fuel_0_layerStyle.qml
            ├── fuel_1_layerStyle.qml
            ├── fuel_2_layerStyle.qml
            ├── kitral_lookup_table.csv
            ├── fbp_lookup_table.csv
            └── spain_lookup_table.csv
```

---
[QGIS]: https://qgis.org
[Repository]: https://github.com/fire2a/fire2a-lib/
[API Documentation]: https://fire2a.github.io/fire2a-lib/src/index.html
[dialog-plugin]: qgis-dialog/README.html
[processing-toolbox-plugin]: qgis-toolbox/README.html
[qgis-cookbook]: qgis-cookbook/README.html
