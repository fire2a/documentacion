---
layout: default
title: Librería de Algoritmos
nav_order: 3
has_toc: false
---
{: .warning}
Código en Python para línea de comandos; Revisa la versión gráfica amigable: [fire2a toolbox](/docs/qgis-toolbox/README.html)
# fire2a-lib
{: .no_toc}
<details closed markdown="block">
  <summary>
    Tabla de contenidos
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

Esta biblioteca es un paquete de python compuesto por nuestros algoritmos relacionados con incendios, utilidades comunes y herramientas para GIS, optimización, agrupación, etc.

Algúnos casos de uso:

* Quieres mirar/usar/adaptar la implementación del Valor de Protección Aguas Abajo?
* Nuevamente olvidaste cómo cargar un ráster .tif en un array numpy + un diccionario de propiedades?
* Necesitas un algoritmo de agrupación de paisajes?

Desarrolladores y académicos son bienvenidos a contribuir!

* [Repositorio]  
* [Documentación API]

## Inicio Rápido
Sugerimos instalar [QGIS] antes de usar, aunque no todos los módulos dependen de él. 
```bash
$ pip install git+https://github.com/fire2a/fire2a-lib.git
$ ipython
In [1]: from fire2a.<presiona-tab-para-ver-submodulos> import <presiona-tab-para-ver-funciones>
```
También revisa las [recetas-qgis] y guías del [Repositorio].
[tl;dr resumen para desarrolladores](/docs/Cell2Fire/README.html#unix-overview)

## Guía del desarrollador
Árbol de componentes principales:
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
│   │   └── fire2template
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
        ├── algorithm....py
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
[Repositorio]: https://github.com/fire2a/fire2a-lib/
[Documentación API]: https://fire2a.github.io/fire2a-lib/src/index.html
[dialog-plugin]: qgis-dialog/README.html
[recetas-qgis]: qgis-cookbook/README.html
