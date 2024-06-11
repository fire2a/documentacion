---
layout: default
title: Creando Cortafuegos
nav_order: 1
has_children: false
has_toc : false
parent: QGIS Fire Analytics Toolbox
---
# Creando Cortafuegos

Cell2FireW acepta un archivo csv que define las celdas no quemables, esto es más fácil que modificar el raster de combustibles cada vez.

Aún más amigable, el toolbox implementa el parseo de los valores 1 de un raster para escribirlo y pasarlo al simulador.

![](img/algo_sim-firebreak_sample.gif){: width="32%" }

## Pasos

1. Crear un raster con las mismas dimensiones que la instancia
2. Poner unos en las celdas que no se queman, esto se puede lograr 'pintando' usando serval, o por la salida de uno de nuestros algoritmos de optimización de decisiones.
3. Seleccionar el raster creado en el desplegable de entrada 'Firebreak'

![](img/create_firebreak.gif){: width="90%" }

## Detalles

Cell2FireW acepta un archivo csv que define las celdas no quemables, esto es más fácil que modificar el raster de combustibles cada vez.

Esto se hace añadiendo un archivo `.csv` al comando de simulación. Por ejemplo: `--FirebreakCells fbv.csv`, conteniendo:

        Year,Ncell
        1,1,81,161,162

Los valores representan un cortafuegos en forma de "L": la celda superior izquierda es 1, la de abajo 81, la de abajo 161, a la derecha 162. (en un raster de 80 pixeles de ancho)

Los encabezados son: Year, Ncell.
La primera columna siempre es Year, 1 (ya que CFW-W solo soporta un fuego antes de reiniciar el paisaje).
Los valores no quemables se colocan como una fila de id de celdas (empezando desde 1)

