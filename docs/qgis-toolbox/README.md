---
layout: default
title: QGIS Fire Analytics Toolbox
nav_order: 1
has_children: true
has_toc : false
---
<h1>
Fire Analytics Toolbox
</h1>
{: .no_toc}
<details closed markdown="block">
  <summary>
    Tabla de contenidos
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>
# Resumen
Nuestra investigación aplicada en incendios como **herramientas gráficas GIS amigables para el usuario**:
- *Simula* incendios forestales a gran escala usando Cell2Fire++
- Obtén *métricas* de amenaza y riesgo
- Usa el *sistema de soporte a la decisión* de ubicación de cortafuegos
- *Combina* nuestros algoritmos con cualquier otro [QGIS] fácilmente

Sin salir del entorno gráfico de [QGIS], solo instalando nuestro **plugin de algoritmos de procesamiento** *fire2a-toolbox*.

Este tipo de plugins difiere de los plugins regulares -al ser mucho más que un cuadro de diálogo emergente- porque siguen una arquitectura de *pipeline de ciencia de datos*.
Delimita claramente: entradas, salidas, algoritmos y contextos; logrando una integración perfecta con todos los algoritmos proporcionados en la [caja de herramientas], proporcionando 5 formas de ser ejecutado.

# Alternativas de uso
1. Tan simple como *llenar un **[cuadro de diálogo]*** (casillas de verificación, menús desplegables, selección de archivos, etc.); siendo las entradas mínimas un ráster de combustible y un escenario climático.
2. **[Lote de formularios]**: Ejecuta ejecuciones secuenciales configurándolas en estilo de hoja de datos donde cada fila es un formulario (mostrado en columnas), *experimenta fácilmente sensibilidades de parámetros*.
3. Como parte de un **[flujo de trabajo de modelo] gráfico**: Arrastra y suelta cajas de parámetros y algoritmos, conecta flechas como entradas-salidas entre ellos, en un [personalizado] *GIS-data-science-pipeline*.
4. Desde una **herramienta de línea de comandos**, ejecuta `qgis_process` [envoltura cli] para llamar a cualquier algoritmo de procesamiento *sin sobrecarga gráfica de QGIS*.
5. **Script de Python**, trabajando *tanto* [llamándolo] desde la [consola de python] de QGIS *o* como [código independiente]

# Instalación
[Guía completa aquí](/docs/docs/qgis-cookbook/README.html) o resumen:
1. [QGIS] versión > 3.28.12 (la versión LTR es en su mayoría compatible pero carece, por ejemplo, de agrupación de resultados de simulación; se recomienda la última versión)
2. La instalación de fire2a-toolbox casi se puede hacer directamente desde el **[gestor de plugins]** de QGIS *pero*:
    - Las [dependencias][requirements.txt] de Python deben resolverse manualmente  
    - El enlace del repositorio/tienda de plugins de fire2a [enlace][toolbox-server] debe agregarse como una fuente de plugins personalizada (*)

**¡Listo!** *El icono de fire2a-toolbox <img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/bonfire.svg"  alt='icon-missing' style="height: 16px"> aparecerá en la lista de algoritmos del Panel de la Caja de Herramientas de Procesamiento*

(*) : Debido a que contiene código binario c++ compilado -para el simulador Cell2Fire, pero el código binario no se puede verificar fácilmente, por lo que el plugin no se permite en el [repositorio/tienda](https://plugins.qgis.org/). Sin embargo, todo nuestro código es de código abierto, su compilación es "reproducible" por una acción automatizada; todo se puede auditar en [fire2a@github](

* **Probadores** deben instalar por archivo `.zip` desde las [versiones][toolbox-releases] de fire2a-toolbox
* **Desarrolladores** deben clonar nuestros repos ([toolbox-repo], [c2f-repo], [fire2a-lib-repo]), compilar cell2fire, hacer un enlace simbólico y configurar dependencias de python adicionales para contribuir ([tl;dr](/docs/docs/Cell2Fire/README.html#unix-overview))

# Primer ejecución de prueba
(¡Mira el gif al final!) Obtener o generar un ráster de modelo de combustible puede ser desafiante (próximamente tutorial), por lo que la forma más simple es:

1. Usar el algoritmo de descarga <img src="./img/downloader.svg"  style="height: 16px"> para obtener una instancia preparada
2. Guardar un [proyecto] vacío en la carpeta descargada (donde están los archivos de combustible, elevación y Weather.csv)
3. Arrastrar y soltar capas desde el inicio del proyecto (Panel de Explorador de archivos) al Panel de Capas
4. Establecer el mismo SRC a las capas y al proyecto (cualquiera en metros es suficiente)
5. Abrir el algoritmo del simulador <img src="./img/forestfire.svg"  style="height: 16px">, seleccionar el modelo de combustible adecuado (Canadá, Kitral o S&B), seleccionar la capa de combustible en el menú desplegable de combustible, presionar ejecutar.

<a name="anchor">
![](img/first_run.gif){: width="75%" }
</a>

Nota: El paso 2 se puede omitir, pero es engorroso seleccionar cada capa desde los exploradores de archivos que usar el menú desplegable para seleccionar entre las capas cargadas actualmente; Además, `Weather.csv` se selecciona automáticamente cuando hay un proyecto guardado.

![](img/algo_sim-first_run.gif){: width="95%" }

# Algoritmos desplegados

**Fire Analytics Toolbox** <img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/bonfire.svg"  alt='icon-missing' style="height: 16px">

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/forestfire.svg"  alt='icon-missing' style="height: 16px">
: [(Cell2)Fire Simulator](./algo_simulator.html)

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/downloader.svg"  alt='icon-missing' style="height: 16px">
: (Simulator) Instances Downloader

**Decision optimization**

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/firebreakmap.svg"  alt='icon-missing' style="height: 16px">
: [Raster knapsack optimization](./algo_knapsack.html)

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/firebreakmap.svg"  alt='icon-missing' style="height: 16px">
: Polygon knapsack optimization : Optimiza el problema clásico de la mochila utilizando polígonos con atributos de valores y/o pesos, devuelve una capa de polígonos con los polígonos seleccionados.

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/firebreakmap.svg"  alt='icon-missing' style="height: 16px">
: Polygon treatment optimization : Usando posibles tratamientos para cada polígono, maximiza el valor cambiado de los polígonos tratados

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/firebreakmap.svg"  alt='icon-missing' style="height: 16px">
: Raster treatment optimization : Maximiza el valor cambiado del ráster tratado, decidiendo qué tratamiento aplicar a cada píxel (o sin cambios), sujeto a restricciones de presupuesto y área

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/firebreakmap.svg"  alt='icon-missing' style="height: 16px">
: Raster treatment & teams optimization : Maximiza el valor cambiado del ráster tratado, decidiendo qué tratamiento aplicar por qué equipo a cada píxel (o sin cambios), sujeto a restricciones de presupuesto, área y capacidades del equipo

**Simulator Post Processing (simpp)**

Bundle: Todos los post procesamientos combinados para conveniencia

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/ignitionpoint.svg"  alt='icon-missing' style="height: 16px">
: Ignition Point(s)

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/bodyscar.svg"  alt='icon-missing' style="height: 16px">
: (Propagation) Fire Scar(s)

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/burntime.svg"  alt='icon-missing' style="height: 16px">
: Propagation Digraph

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/fireface.svg"  alt='icon-missing' style="height: 16px">
: Spatial Statistics, cualquiera de: Hit Rate Of Spread, Flame Length, Byram Fire Line Intensity, Crown Fire Scar, Crown Fire Fuel Consumption Ratio, Surface Burn Fraction

**simpp Risk Metrics**

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/dpv.svg"  alt='icon-missing' style="height: 16px">
: DownStream Protection Value

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/bc.svg"  alt='icon-missing' style="height: 16px">
: Betweenness Centrality

<img src="https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/assets/bodyscar.svg"  alt='icon-missing' style="height: 16px">
: Burn Probability

**Auxiliariares**

Match AII Grid Rasters : Simplifica el uso de gdal translate tres veces, para recortar la extensión, luego redimensionar y reemplazar el geotransform para que coincida con un ráster ascii en otro


---
[QGIS]: https://qgis.org

[requirements.txt]: https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/fireanalyticstoolbox/requirements.txt 
[requirements.dev.txt]: https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/requirements.dev.txt

[Scott&Burgan-dialog-server]: https://fdobad.github.io/qgis-processingplugin-template/plugins.xml
[Kitral simulator dialog-server]: https://fdobad.github.io/fire2am-kitral/plugins.xml 
[toolbox-repo]: https://www.github.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin
[c2f-repo]: https://www.github.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin
[fire2a-lib-repo]: https://www.github.com/fire2a/fire2a-lib


[graphical model]: https://docs.qgis.org/latest/en/docs/user_manual/processing/modeler.html
[toolbox]: https://docs.qgis.org/latest/en/docs/user_manual/processing/toolbox.html
[form dialog]: https://docs.qgis.org/latest/en/docs/user_manual/processing/toolbox.html#the-algorithm-dialog
[Batch of forms]: https://docs.qgis.org/latest/en/docs/user_manual/processing/batch.html#processing-batch
[cli wrapper]: https://docs.qgis.org/latest/en/docs/user_manual/processing/standalone.html
[python console]: https://docs.qgis.org/latest/en/docs/user_manual/plugins/python_console.html#console
[calling it]: https://docs.qgis.org/latest/en/docs/user_manual/processing/console.html
[standalone code]: https://raw.githubusercontent.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/main/script_samples/standalone.py
[custom]: https://github.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/tree/main/graphical_models
[plugin manager]: https://docs.qgis.org/latest/en/docs/training_manual/qgis_plugins/fetching_plugins.html

[toolbox-server]: https://fire2a.github.io/fire-analytics-qgis-processing-toolbox-plugin/plugins.xml
[toolbox-releases]: https://github.com/fire2a/fire-analytics-qgis-processing-toolbox-plugin/releases
[project]: https://docs.qgis.org/3.28/en/docs/user_manual/introduction/project_files.html
