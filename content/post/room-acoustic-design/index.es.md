---
author: "Matías Di Bernardo"
title: "Diseño de un auditorio"
date: "2022-06-22"
description: "Diseño de un auditorio sin refuerzo sonoro centrandose en la acústica del recinto."
categories: [
    "Acoustics",
]
tags: [
    "University",
]
image: "front.PNG"
---

Este proyecto es el trabajo final de la clase *Acústica y Psicoacústica II*, donde se nos encargó rediseñar un auditorio existente. El objetivo era aplicar la teoría vista en clase para crear un auditorio optimizado desde el punto de vista acústico. Para nuestro proyecto, elegimos rediseñar el Royal Albert Hall en Londres. Esto representó un desafío particular debido a las grandes dimensiones del auditorio, lo que dificulta asegurar que el sonido llegue de manera uniforme a todos los espectadores.

## Ideas Principales del Rediseño
El rediseño buscó preservar el concepto original del auditorio, incluyendo su gran volumen y capacidad de asientos, mientras se introducían cambios críticos para mejorar su acústica. Aunque el enfoque principal fue la mejora acústica, el rediseño también consideró otros factores esenciales, como las líneas de visión y una distribución adecuada de los asientos.

A pesar de la intención de mantener las dimensiones originales del auditorio, su volumen resultó ser demasiado grande para lograr un tiempo de reverberación óptimo. Para abordar este problema, el rediseño incorporó un techo intermedio para reducir el volumen del techo esférico, y se redujo el área principal de asientos. Estos cambios permitieron obtener un mejor tiempo de reverberación en la sala, como se ilustra en la sección transversal a continuación.

![Sección transversal del rediseño del auditorio](cross_section.PNG)

## Detalles de Construcción y Regulaciones
Para garantizar un rediseño factible y funcional, se consideraron cuidadosamente los siguientes aspectos clave:
- Distribución de asientos
- Espaciado de los pasillos
- Optimización de las líneas de visión
- Comodidad del escenario

## Tratamiento Acústico
El tratamiento acústico fue la parte más crítica de este estudio y se centró en dos aspectos principales: reflexiones y tiempo de reverberación.

### Reflexiones
El análisis de las reflexiones es esencial para la experiencia acústica del público. El Royal Albert Hall original cuenta con un techo esférico que centraliza las reflexiones, creando efectos acústicos indeseables. Para mitigar esto, el rediseño incorporó un techo intermedio con una geometría específica diseñada para distribuir las reflexiones de manera uniforme entre el público.

El diseño escalonado del techo garantiza reflexiones adecuadas para todas las filas de asientos. En el balcón principal, se abordaron dos reflexiones específicas para compensar el menor nivel de presión sonora (SPL) debido a la gran distancia desde el escenario, como se muestra en la imagen a continuación.

![Reflexiones en el techo del balcón](balcony_cel_ref.PNG)

También se optimizaron las reflexiones laterales mediante ajustes en la geometría del escenario y las paredes de los balcones laterales.

![Reflexiones laterales en el público principal](lateral_ref.PNG)

Además, el rediseño buscó minimizar el ITDG (Initial Time Delay Gap) en los diferentes puntos del público.

### Materiales y Tiempo de Reverberación
El rediseño siguió las recomendaciones del libro *Acoustic Absorbers and Diffusers* para lograr un equilibrio entre absorción, difusión y reflexiones especulares. Se utilizaron materiales reflectantes en el techo y en partes de los balcones laterales para garantizar reflexiones especulares efectivas. Para reducir el tiempo de reverberación (RT), se aplicaron materiales con coeficientes de absorción más altos en otras superficies.

Usando los materiales seleccionados y la ecuación de Sabine, calculamos el RT estimado del auditorio. El tiempo de reverberación para las diferentes frecuencias se muestra a continuación:

![Tiempo de reverberación por frecuencia](rt.PNG)

El RT calculado para frecuencias medias es de 2,51 segundos. Aunque este valor está ligeramente por encima del máximo recomendado de 2,4 segundos para una acústica óptima, es aceptable dado el gran volumen del auditorio.

## Modelado 3D
Renderizamos el auditorio rediseñado utilizando el software *SketchUp*. A continuación, se presentan algunas visualizaciones:

{{< carousel-royal items="1" height="450" unit="px" duration="70000" >}}

## Conclusiones
Rediseñar el Royal Albert Hall para mejorar su acústica mientras se preserva su esencia original presentó desafíos significativos. El proyecto requirió soluciones innovadoras para abordar los problemas acústicos sin comprometer el diseño icónico del auditorio. Aunque fueron necesarios algunos cambios, el resultado final demuestra un rediseño cuidadosamente pensado que mejora la acústica mientras mantiene el carácter histórico del Royal Albert Hall. Este proyecto también profundizó nuestra comprensión de los conceptos de acústica y diseño de auditorios.

Una descripción detallada de este proyecto está disponible en el siguiente [artículo](https://drive.google.com/file/d/1CkX-t_gx2s_YlKbrjB-5IK_dmZIkpJrd/view?usp=sharing) (en inglés).
