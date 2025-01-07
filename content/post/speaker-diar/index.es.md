---
author: "Matías Di Bernardo"
title: "Evaluación de diferentes modelos de Separación del Hablante"
date: "2022-11-04"
description: "Evaluación e implementación de diferentes modelos de Speaker Diarization con redes neuronales siamésas."
categories: [
    "Deep Learning",
]
tags: [
    "Personal Project",
]
---

Este proyecto comenzó como el trabajo final para un seminario de la UNTREF llamado *Seminario en Aplicaciones de Redes Neuronales en la recuperación de información musical*. El objetivo era utilizar una Red Neuronal Siamés (SNN, por sus siglas en inglés) en un contexto diferente al visto en clase (detección de similitud musical).

Para el proyecto final de este curso, desarrollamos un modelo SNN desde cero utilizando el framework *Keras* y la arquitectura *SincNet* para reducir la dimensionalidad del audio, logrando buenos resultados. Más adelante, para expandir este proyecto, probé otro enfoque utilizando *Wav2Vec* para la reducción de dimensionalidad y reimplementé todo el proyecto en el framework *PyTorch*. Sin embargo, este intento arrojó resultados subóptimos, lo que indica que la reducción de dimensionalidad con Wav2Vec perdió información crítica necesaria para la tarea de diarización de locutores.

## Tarea de Diarización de Locutores
El objetivo de un modelo de diarización de locutores es identificar diferentes hablantes en un flujo de audio que contiene múltiples voces. Por ejemplo, en un podcast con dos personas (A y B), el modelo debe determinar los pasos de tiempo en los que el hablante A está hablando y los pasos de tiempo en los que el hablante B está hablando (e identificar implícitamente los períodos de silencio). Estos modelos son extremadamente útiles para la edición de audio y el análisis de largas secuencias de audio con múltiples hablantes.

## ¿Por qué Redes Neuronales Siamés?
En clase, exploramos la arquitectura siamés para comparar similitudes entre piezas musicales, desarrollando una herramienta capaz de identificar versiones de canciones famosas.

Una Red Neuronal Siamés consiste en dos o más subredes idénticas que comparten los mismos pesos y parámetros. Está diseñada para comparar pares de entradas y medir su similitud, generalmente utilizando una métrica de distancia como la distancia euclidiana. Cada subred procesa una entrada, y las salidas se combinan para calcular un puntaje de similitud.

Con esta comparación de similitudes en mente, quisimos aplicar estas redes a la tarea de diarización de locutores. La idea era generar embeddings de hablantes a partir de audio utilizando un modelo preentrenado y comparar las salidas de diferentes segmentos de audio. Basándonos en el puntaje de similitud, buscamos identificar los segmentos donde diferentes hablantes están hablando.

## Experimentos
Probé dos métodos diferentes para la extracción de características de audio que servirían como embeddings de hablantes.

### Implementación en Keras con SincNet
En este enfoque, utilizamos la arquitectura SincNet para extraer características específicas de los hablantes a partir del audio. SincNet aplica funciones sinc aprendibles como sus filtros, que son particularmente adecuadas para el procesamiento de audio, ya que imitan los filtros de paso de banda tradicionales. Estas características se introdujeron en la Red Neuronal Siamés, que comparó pares de segmentos de audio para calcular sus puntajes de similitud. El modelo se entrenó con conjuntos de datos de audio etiquetados y observamos un rendimiento sólido al agrupar segmentos de audio por hablante, logrando límites claros entre diferentes hablantes.

Un informe con los resultados puede encontrarse en el siguiente [notebook de Jupyter](https://github.com/MatiasDiBernardo/Speaker-Diarization-with-SNN/blob/master/TP%20Final%20Seminario%20Redes%20-%20Di%20Bernardo%20Ferreyra.ipynb) (en español).

### Implementación en PyTorch con Wav2Vec
Para este método, utilicé Wav2Vec, un modelo preentrenado poderoso para la extracción de embeddings profundos de audio. A diferencia de SincNet, los embeddings de Wav2Vec se derivan del aprendizaje autosupervisado, capturando representaciones de alto nivel del audio. Estos embeddings se usaron en la Red Neuronal Siamés para comparaciones de similitud. Sin embargo, los resultados fueron subóptimos para la tarea de diarización. Parece que Wav2Vec, aunque excelente para tareas de reconocimiento de voz, perdió algunos detalles específicos del hablante necesarios para distinguir entre diferentes voces en nuestro contexto.

## Resultados
Los experimentos demostraron que la elección del método de extracción de características es crucial para la diarización de locutores. La implementación en Keras con SincNet superó a la implementación en PyTorch con Wav2Vec, mostrando mayor precisión al identificar transiciones entre hablantes. Esto sugiere que la extracción de características específicas para la tarea, como SincNet, es más efectiva que los embeddings de propósito general como Wav2Vec para la diarización de locutores.

El código de este proyecto está disponible en este [repositorio](https://github.com/MatiasDiBernardo/Speaker-Diarization-with-SNN).

## Conclusiones
Este proyecto fue una de mis primeras experiencias con modelos de aprendizaje profundo, donde apliqué mis conocimientos a un problema sin seguir un artículo específico o utilizar un modelo preentrenado. Exploré diferentes soluciones y concluí sobre la importancia de la extracción de características y la selección del modelo.

También me ayudó a familiarizarme con la sintaxis de los frameworks de aprendizaje profundo más populares y a solidificar mi comprensión en el proceso.
    