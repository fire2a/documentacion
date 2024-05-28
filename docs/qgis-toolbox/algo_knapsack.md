---
layout: default
title: Raster knapsack optimization
nav_order: 2
has_children: false
has_toc : false
parent: QGIS Fire Analytics Toolbox
---
## Optimización de la mochila de ráster
### Introducción
_Una integración de prueba de concepto de solucionadores de programación matemática para modelar y resolver problemas de optimización con entidades GIS._

Los usuarios pueden crear una nueva capa de ráster que seleccione los píxeles más valiosos en un ráster, de acuerdo con una restricción de capacidad definida por otro ráster -opcional- y una proporción fraccional.

Varios solucionadores pueden ser utilizados (cbc, glpk, cplex_direct, gurobi, ipopt, NEOS, etc.), gracias a que el MIP se modela y resuelve a través de [pyomo](http://www.pyomo.org).

Antes de ejecutar este algoritmo, asegúrese de haber instalado los solucionadores correspondientes que desee utilizar. Consulte la [documentación de pyomo](https://pyomo.readthedocs.io/en/stable/installation.html#conditional-dependencies) para obtener más detalles.

| captura de pantalla |
| --- |
|<img src="img/algo_knapsack_screenshot.png"  alt='no se puede cargar la imagen' height=400px >|

### Descripción detallada
Al seleccionar una capa de Valores y/o una capa de Pesos, y establecer el límite en la capacidad total, se crea una capa que maximiza la suma de los valores de los píxeles seleccionados.

La restricción de capacidad se establece eligiendo una proporción (entre 0 y 1), que multiplica la suma de todos los pesos (excepto no-data). Por lo tanto, 1 selecciona todos los píxeles que no son no-data en ambas capas.

Este problema de la mochila de ráster es NP-duro, por lo que se utiliza un motor de solución MIP para encontrar "casi" la solución óptima, porque -a menudo- es asintóticamente difícil probar el valor óptimo. Por lo tanto, un margen predeterminado del 0,5% y un límite de tiempo de 5 minutos cortan la ejecución del solucionador. El usuario puede experimentar con estos parámetros para equilibrar entre precisión, velocidad y tamaño de la instancia(*). ¡En Windows, cerrar la ventana de terminal en blanco abortará la ejecución!

Al usar Pyomo, se pueden utilizar varios solucionadores MIP: CBC, GLPK, Gurobi, CPLEX o Ipopt; Si son accesibles a través de la ruta del sistema, de lo contrario, el archivo ejecutable puede ser seleccionado por el usuario.

La instalación de los solucionadores(solvers) es responsabilidad del usuario, aunque la versión de Windows se incluye con binarios no firmados de CBC, por lo que sus usuarios verán una advertencia de "Windows protegió su PC", evite presionar el botón "No ejecutar", siga el enlace "Más información", desplácese y luego presione "Ejecutar de todos modos".

(*): La complejidad puede reducirse en gran medida reescalando y/o redondeando los valores en enteros, o incluso mejor, coarsando la resolución del ráster (ver gdal translate resolution).
