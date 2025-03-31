---
author: "Matías Di Bernardo"
title: "IA Generativa, Flow Matching y TTS"
date: "2025-03-24"
description: "Conceptos mas importantes de una presentación que dí sobre F5-TTS, un modelo de TTS que utiliza Flow Matching."
categories: [
    "Math",
    "Deep Learning",
]
tags: [
    "Work",
]
image: "front2.png"
---

En *Intercambios Transorgánicos*, trabajamos continuamente con modelos de *Deep Learning* de última generación. Para ello, nos mantenemos en constante aprendizaje sobre los desarrollos más recientes en el campo. En esta presentación, el objetivo fue explicar los fundamentos del modelo *F5-TTS*, un sistema de síntesis de voz de vanguardia. Durante el desarrollo, se introdujo el concepto de inteligencia artificial generativa y los modelos de flujo (*flow-based models*), dado que *F5-TTS* se basa en esta técnica. El propósito es compartir este conocimiento con el equipo y con cualquier persona interesada en iniciarse en los modelos de conversión de texto a voz (*Text-to-Speech*).

## Introducción - IA Generativa y TTS
La estructura de la clase se organizó de la siguiente manera:

1. **Introducción a los modelos de TTS**: Se describen los diferentes modelos utilizados, sus principales características y las razones por las cuales se decidió cambiar de enfoque.
2. **Evolución de los modelos TTS**: Se presenta un gráfico basado en encuestas que muestra la evolución de diversas tecnologías de TTS.
3. **Cambio de paradigma en modelos de lenguaje**: Se explica cómo el uso de grandes volúmenes de datos ha permitido una mejor generalización en modelos de lenguaje.
4. **Ejemplo de generalización**: Se presentan casos ilustrativos, como la generación de una imagen de un astronauta montando un caballo, ejemplos de audio y síntesis de acentos específicos (ej., un hablante cordobés enojado).
5. **Cambio en la estructuración de conjuntos de datos**:
    - **Enfoque tradicional**: Uso de un único hablante de alta calidad con gran cantidad de datos (modelo entrenado para cada hablante).
    - **Enfoque actual y futuro**: Uso de conjuntos de datos diversos con etiquetas que permiten entrenar modelos capaces de entender el concepto del habla y generalizar en múltiples tareas (ejemplos extraídos de *VoiceBox*).
    - **Costo computacional**: Se menciona el aumento en el tamaño de los modelos y la dificultad de su entrenamiento, similar a los modelos de lenguaje a gran escala (*LLMs*).
6. **Explicación de IA Generativa**:
    - Introducción a los modelos generativos y el concepto de distribución subyacente.
    - Explicación sobre *Transformers* y su función en la clasificación con contexto. Se aclara que aunque los *Transformers* son modelos *Non-Autoregressive* (NAR) en entrenamiento, en inferencia funcionan de manera *Autoregressive* (AR).
    - Diferencia entre modelos de clasificación y modelos generativos basados en reducción de dimensionalidad y variables latentes.

## Modelos de TTS: VoiceBox, E2 y F5
Esta sección detalla los principales avances en modelos de TTS que han llevado al desarrollo de *F5-TTS*.

### 1. VoiceBox TTS - *In Context Learning*
Se introduce la arquitectura inicial de *VoiceBox*, cuyo objetivo principal es la generalización mediante *In Context Learning*. Este enfoque permite al modelo inferir información a partir de ejemplos previos. Para lograrlo, se le proporciona un fragmento de audio con una parte oculta, forzando al modelo a completarla de manera coherente.

> *"We show that Voicebox’s text-guided speech infilling approach is much more scalable in terms of data while subsuming many common speech generative tasks."*

Este método, introducido por Meta en *VoiceBox*, marca un cambio de paradigma al demostrar que los modelos de TTS pueden beneficiarse de técnicas previamente utilizadas en modelos de lenguaje e imagen.

No obstante, el modelo aún depende de técnicas clásicas en TTS, como el predictor de duración de fonemas y el *Forced Alignment* para mapear fonemas a espectrogramas de Mel, ya que la longitud de estos no coincide con la de los tokens de texto.

### 2. E2 TTS - *Filler Tokens*
*E2 TTS* simplifica varias de las decisiones arquitectónicas de *VoiceBox*, especialmente en lo referente a la longitud de los espectrogramas de Mel y el texto. En lugar de utilizar alineación forzada, introduce los *Filler Tokens*, que permiten igualar la dimensión entre texto y audio de manera más sencilla. Esta estrategia facilita que el modelo aprenda la asociación temporal entre ambos elementos.

Otro cambio significativo es que el modelo trabaja directamente con texto en lugar de fonemas. Aunque esto podría parecer una desventaja (dado que palabras homógrafas pueden tener pronunciaciones diferentes), el contexto provee suficiente información para inferir la pronunciación adecuada, de manera similar al procesamiento del lenguaje natural en humanos.

### 3. F5 TTS - *Open Source*
Si bien *E2 TTS* representa un avance importante, su entrenamiento es lento debido a la necesidad de inferir asociaciones previamente guiadas. *F5 TTS* optimiza el modelo anterior con las siguientes mejoras:

- **Uso de ConvNeXt**: Mejora el procesamiento del texto de entrada.
- **Cambio de arquitectura**: Sustitución de la red *U-Net* por *DiT* (*Diffusion Transformer*).
- **Sway Sampling**: Optimización en el proceso de inferencia.

Además, *F5 TTS* es de código abierto, lo que facilita su adopción y mejora por parte de la comunidad.

## Flow Matching - Fundamentos Teóricos
Para comprender el funcionamiento de *F5-TTS*, es necesario revisar los modelos en los que se basa, conocidos como *Flow Matching Models*. Estos modelos han evolucionado a partir de técnicas previas en modelado de distribuciones probabilísticas.

### 1. Normalizing Flow
Los *Normalizing Flows* son una familia de modelos probabilísticos que transforman una distribución simple en una más compleja mediante una serie de funciones invertibles y diferenciables. Se utilizan para modelar distribuciones de datos de alta dimensión y generar muestras realistas con un control preciso sobre la probabilidad.

### 2. Residual Flow
Los *Residual Flows* extienden los *Normalizing Flows* al permitir transformaciones más flexibles sin necesidad de cumplir estrictamente con la condición de invertibilidad. Esto se logra mediante redes residuales que aproximan las funciones de transformación sin restricciones de estructura.

### 3. Continuous Normalizing Flows (CNF)
Los *Continuous Normalizing Flows* reformulan los *Normalizing Flows* en términos de ecuaciones diferenciales ordinarias (ODEs). En lugar de aplicar transformaciones discretas en pasos sucesivos, estos modelos aprenden una dinámica continua en el espacio latente, lo que permite una mayor expresividad y eficiencia computacional.

### 4. Flow Matching
*Flow Matching* es una técnica que optimiza la transformación de una distribución de referencia a una distribución objetivo utilizando un enfoque basado en la minimización de una función de costo específica. Se diferencia de los enfoques anteriores al no requerir el cálculo explícito de la función de densidad, lo que lo hace especialmente útil para modelos generativos de gran escala, como *F5-TTS*.

## Grabación de la presentación
Cada sección detalla en este artículo se explica en profundidad en la presentación:

{{< youtube YIpvFC41NUw >}}
