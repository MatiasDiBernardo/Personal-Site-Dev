---
author: "Matías Di Bernardo"
title: "Construcción y diseño de un altoparlante personal"
date: "2024-11-20"
description: "Contrucción, diseño, medición y validación de un sistema de sonido hogareño."
categories: [
    "Acoustics",
    "Electronics",
]
tags: [
    "University",
]
image: "front_bass.PNG"
---

# "BassAdo" un parlante hogareño semi portable de bajo costo
Este proyecto se enmarca en la materia Electroacústica II en UNTREF de la carrera Ingeniería de Sonido. La tarea era diseñar desde cero un altoparlante aplicando la teoría y conceptos explicados en clase.
El trabajo se fue desarrollando durante todo el cuatrimestre con diferentes etapas a completar que se tenían que presentar con un informe. El parlante esta pensado para ser usado en un espacio grande, puede ser al aire libre, para poner música en un entorno de reunión. Se lo denomino *Bassado* para combinar el asado (típica comida argentina donde la gente se reune) y la palabra bass, enfatizando la característica del altoparlante.

## Diseño
El objetivo es diseñar un sistema de audio hogareño con prestaciones accesibles, que permita explorar temas de interés abordados en la materia. El diseño busca lograr una predominancia en graves, característica de los sistemas comerciales, priorizando la extensión del ancho de banda en bajas frecuencias por encima de un bajo retardo de grupo y control temporal del sistema.

Con respecto a los transductores a utilizar, el equipo contaba con unidades de la marca Yharo, que se pueden clasificar como no profesionales, consumidor-aficionado, con posibles aplicaciones en automóviles y/o sistemas hogareños.
Se evalúa la respuesta en impedancia de los mismos y se selecciona un Woofer de 8” para cubrir la sección de bajas frecuencias, y dos de 4” para el rango de medias/altas.

Al medir los parámetros de Thielle-Small de los altoparlantes se encuentra que tiene un *Vas* (Volumen Acústico Equivalente de Suspensión) muy alto, lo que requiere realizar un gabinete con mucho volumen para tener un buen control. Para solucionar este problema y dado la posibilidad de que se contaba con 2 Woofers de 8”, se decide hacer un altoparlante del tipo isobárico, colocando los 2 Woofers en serie acústicamente, para que tengan mayor control y poder hacer más chico el gabinete. Además, va a ser un gabinete ventilado para tener mejor respuesta en bajas.

La respuesta de los altoparlantes (paráemtros TS) fue obtenida en el software [REW](https://www.roomeqwizard.com/). Con esos parámetros, se simula en el software [Basta!](https://www.tolvan.com/index.php?page=/basta/basta.php) y se optimizan los parámetros para obtener la respuesta deseada. Lo principal fue sintonizar la frecuencia de resonancia del port, ya que el objetivo del altoparlante era tener una buena respuesta en bajas. El transductor tenía una *fs* en 45 Hz, y se busca sintonizar el port en 40 Hz controlando el largo del tubo y el volumen de aire del gabinete.

En base a estos resultados, se hace un modelo 3D del gabinete en el software [SolidWorks](https://www.solidworks.com/) con el que se manda a cortar las maderas para poder construir el gabinete.

![Modelado 3D del gabinete del altoparlante](diseño_gab.PNG)

El detalle de todo este proceso esta documentado en el siguiente [informe de diseño](https://drive.google.com/file/d/1uej1m6gwg99JoPEw5Jbu3cTq74ViIG58/view?usp=sharing).

## Construcción
Se mandaron a realizar los cortes a las maderas para hacer el gabinete según el modelo 3D y se realiza el ensamblado.

{{< carousel-bassado items="1" height="700" unit="px" duration="700000" >}}

Como se puede ver en las imágenes, se agregó lana de roca para hacer de absorbente acústico. Al realizar las mediciones nos dimos cuenta de que fue demasiado (la resonancia del port quedaba muy amortiguada) pero se le pudo sacar lana de roca hasta lograr el resultado deseado.

## Medición y Calibración
Se realizaron mediciones de respuesta en frecuencia y de directividad en el laboratorio de la universidad, teníamos a disposición el siguiente equipamiento:
- Potencia Powersoft M50Q
- Micrófono Earthworks M50
- Placa de Audio RME Fireface UCX
- Mesa Giratoria OUTLINE ET250-3D

Con estas prestaciones y utilizando el software [Arta](https://artalabs.hr/), se pudo caracterizar la respuesta acústica de los transductores por separado (lo cual nos va a servir para simular los filtros de cruze). También se evalúa la respuesta directiva en el eje vertical y el horizontal para poder determinar cual es la mejor disposición para utilizar el dispositivo. Se realizaron gráficos de la respuesta para los dos transductores. 

![Respuesta polar del driver de medias/altas frecuencias](patron_polar.PNG)

Todas las respuestas y el análisis en profundidad se encuentran en el siguiente [informe de medición](https://drive.google.com/file/d/1dPwJAqadPM3Ja80anA1P1Ei3EP9M8w-q/view?usp=sharing).

## Diseño de filtro de cruce
Por último, se diseña la etapa del filtro de curce. Con las mediciones realizadas previamente, se subieron los datos al software [VituixCad](https://kimmosaunisto.net/). El objetivo del filtro de cruce es lograr una respuesta en frecuencia que suene agradable al reproducir un programa músical y que realce las bajas frecuencias. Se busca también, la mayor homogeneidad en la respuesta polar vertical.

Como se va utilizar una etapa de potencia que requiere alimentación, se va a realizar un filtro de cruce activo con la topología Sallen-Key. Se definen una cantidad de filtros según el espacio y el costo y se realizan los ajustes en el software para obtener la respuesta deseada. Por ejemplo, para los drivers de baja frecuencia se realizó el siguiente arreglo:

![Filtro de cruce para el driver de bajas frecuencias](filtro_cruce.PNG)

Donde:
- F1: Pasa altos fs=30 Hz | Q=0.67
- F2: Pasa bajos fs=480 Hz | Q=0.5
- F3: Elimina Banda 220 Hz
- F4: Elimina Banda 400 x Hz

Antes de realizar el filtro, se probó la configuración planteada con un filtro digital para evaluar de forma práctica la respuesta del sistema según el diseño planteado.
Todos los detalles de esta sección estan plasmados en el siguiente [informe de filtro de cruce](https://drive.google.com/file/d/121wkPnp_QsODk99a2Jm44jfb-Xbl6ZKn/view?usp=sharing).

## Conclusiones
Con este trabajo, pudimos bajar muchos conceptos teóricos a la práctica y entender con más profundidad como es el desarrollo y los desafíos en un diseño de un sistema electroacústico.
