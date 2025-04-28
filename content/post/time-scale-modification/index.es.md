---
author: "Matías Di Bernardo"
title: "Algorítmos de modificación de escala temporal"
date: "2023-03-09"
description: "Evaluación y desarrollo de diferentes algorítmos de TSM en Python."
categories: [
    "Programming",
    "DSP",
]
tags: [
    "Academic",
    "University",
]
image: "tsm.PNG"
---
Los algoritmos de modificación de escala temporal se utilizan para acelerar o desacelerar la velocidad de reproducción de un audio. Cuando se cambia la tasa de muestreo de un audio, la velocidad cambia, pero también lo hace el tono (al acelerar el audio, suena con un tono más alto). Existen diferentes algoritmos que permiten modificar la velocidad del audio manteniendo constante el tono.

La principal referencia para este estudio es el siguiente artículo, donde se describen en detalle los distintos algoritmos.

> A Review of Time-Scale Modification of Music Signals.<br>
> — <cite>Jonathan Driedger y Meinard Müller[^1]</cite>

[^1]: A Review of Time-Scale Modification of Music Signal [paper](https://www.researchgate.net/publication/295082364_A_Review_of_Time-Scale_Modification_of_Music_Signals).

## Comparación de algoritmos
Existen dos algoritmos principales, el *Overlap-and-add* (OLA) y el *Phase Vocoder* (PV). Ambos logran buenos resultados bajo diferentes señales y condiciones. Para aprovechar las ventajas de ambos métodos, se utiliza una implementación final basada en la *Separación Armónico-Percusiva* (HPS), que combina ambos algoritmos y logra los mejores resultados.

### OLA
Este método trabaja en el dominio del tiempo, superponiendo secciones del audio (ventanas) y reorganizándolas para lograr un cambio deseado en la velocidad. Este método funciona bien para señales percusivas, pero introduce artefactos cuando se utiliza con señales armónicas o tonales.

### PV
Este método opera en el dominio de la frecuencia, combinando fragmentos de audio en este dominio para lograr el cambio deseado en el tiempo. Utiliza el principio del vocoder de fase para propagar la fase entre ventanas, garantizando la continuidad al aplicarse a señales armónicas. Sin embargo, no es efectivo para señales percusivas, ya que el proceso de propagación de fase elimina los transitorios en las señales.

Creé visualizaciones usando *Manim* para mejorar mi presentación en clase. El primer video muestra cómo el algoritmo PV alinea las ventanas para garantizar transiciones suaves en la señal generada a lo largo del tiempo. Para lograrlo, se aplica una ventana gaussiana que mantiene la continuidad y suavidad, incluso al inicio y al final de la secuencia.

{{< vimeo 1045495557 >}}

El segundo video muestra los efectos de aplicar el algoritmo PV a una señal que contiene transitorios.

{{< vimeo 1045495634 >}}

Como predice la teoría, los transitorios desaparecen porque el algoritmo PV interrumpe la alineación vertical de la fase. Aunque estos ejemplos utilizan señales idealizadas, demuestran de manera efectiva las principales fortalezas y limitaciones del algoritmo.

### HPS
Para utilizar ambos métodos con las señales ideales, se emplea el algoritmo HPS. Este algoritmo separa la señal en sus componentes armónicas y percusivas. Funciona comparando la continuidad de la señal en la representación STFT, utilizando un filtro que compara la presencia vertical contra la horizontal en el espectrograma. Con un umbral, se puede definir una máscara binaria sobre el espectrograma para separar las partes percusivas de las secciones armónicas.

## Resultados
Implementamos con éxito todos los algoritmos y los comparamos, verificando los contenidos teóricos presentados en el artículo de referencia. Durante el proceso, desarrollamos un conjunto de herramientas para utilizar estos algoritmos con el lenguaje de programación Python. Todo el código está disponible en este [repositorio](https://github.com/MatiasDiBernardo/TSM_Toolkit).

## Presentación académica
El estudio fue presentado junto a mis compañeros en las *JAAS* (Jornadas de Acústica, Audio y Sonido). Las principales ideas y conclusiones se expusieron en la conferencia. En el siguiente informe se encuentran todos los detalles y análisis realizados para este proyecto (en español).

> ALGORITMOS DE MODIFICACIÓN DE ESCALA TEMPORAL.<br>
> — <cite>Matías Di Bernardo; Matías Vereertbruhggen; Sebastían Carro[^2]</cite>

[^2]: JAAS 2023 - Algoritmos de Modificación de Escala Temporal [paper](https://drive.google.com/file/d/12kPB3qBjczyx7X2XV3ZpBDo1GDO2u4qR/view?usp=sharing).
