---
author: "Matías Di Bernardo"
title: "Entendiendo FastPitch y la arquitectura Transformers"
date: "2023-08-23"
description: "Preparación de una clase para entender el modelo de TTS FastPitch centrandome en la arquitectura Transformer."
categories: [
    "Math",
    "Deep Learning",
]
tags: [
    "Work",
]
image: "front.png"
---

Entender un modelo moderno de deep learning no es sencillo debido a la gran cantidad de conocimiento previo necesario y al rápido ritmo de avance en este campo. En el proyecto de investigación *Intercambios Transorgánicos*, estamos trabajando con TTS, específicamente con el modelo FastPitch de Nvidia. He estudiado este modelo para ajustarlo (fine-tuning) al español y he compartido este proceso de investigación en una clase para ayudar a mis colegas del grupo de investigación a comprenderlo mejor.

## Entendiendo los Modelos Seq2Seq
En *Intercambios Transorgánicos* utilizábamos previamente Tacotron2 como modelo TTS. Este modelo funciona bien, pero presenta varios problemas, principalmente durante el entrenamiento y la inferencia, debido a su naturaleza auto-regresiva. En contraste, FastPitch es un modelo no auto-regresivo (NAR). Para entender estas diferencias, exploré en profundidad los modelos seq2seq, analizando su evolución a lo largo del tiempo, y realicé un resumen rápido de los modelos de análisis de secuencias más relevantes:

- RNN  
- LSTM  
- Transformers  

Tacotron2 se basa en un modelo LSTM (AR), mientras que FastPitch utiliza Transformers (NAR). Comprender esta progresión tecnológica proporciona un contexto esencial, especialmente sobre los transformers, incluyendo la codificación posicional, un elemento clave para su naturaleza no auto-regresiva, y el mecanismo de atención.

## La Arquitectura Transformer
Comencé estudiando la arquitectura transformer, ya que es fundamental para el modelo FastPitch. Revisé recursos en línea y el influyente artículo *Attention is All You Need*. A continuación, algunos puntos clave que anoté durante mi estudio:

1. **Mecanismo de Auto-Atención**  
   - **Propósito**: Focalizar dinámicamente en diferentes partes de la secuencia de entrada.  
   - **Mecanismo**:  
     - Query (Q), Key (K), Value (V): Derivados de las embeddings de entrada.  
     - Los puntajes de atención se calculan como el producto punto de Q y K, escalado por la raíz cuadrada de la dimensión.  
     - Los puntajes se normalizan con softmax para generar pesos de atención.  
     - Se calcula una suma ponderada de V basada en estos pesos para producir la salida.  

2. **Atención Multi-Cabezal**  
   - **Propósito**: Capturar diferentes relaciones entre tokens aplicando múltiples mecanismos de auto-atención en paralelo.  
   - **Mecanismo**: Las salidas de las múltiples cabezas de atención se concatenan y se transforman linealmente.  

3. **Codificación Posicional**  
   - **Propósito**: Añadir información sobre el orden de los tokens en la secuencia, compensando la falta de un concepto incorporado de orden secuencial en los Transformers (a diferencia de los RNNs).  
   - **Mecanismo**: Se añade un vector fijo o aprendible a las embeddings de entrada.  

4. **Estructura Codificador-Descodificador**  
   - **Codificador**: Procesa la secuencia de entrada en representaciones ricas en contexto.  
     - Componentes:  
       - Auto-atención multi-cabezal  
       - Red neuronal feed-forward (FFN)  
       - Normalización por capas y conexiones residuales  
   - **Descodificador**: Genera la secuencia de salida atendiendo tanto a las salidas del codificador como a los tokens generados previamente.  
     - Componentes:  
       - Auto-atención multi-cabezal enmascarada (evita atender a tokens futuros)  
       - Atención multi-cabezal sobre las salidas del codificador  
       - FFN, normalización por capas y conexiones residuales  

5. **Red Feed-Forward (FFN)**  
   - **Propósito**: Introducir no linealidad y procesar cada token de manera independiente.  
   - **Mecanismo**: Dos capas lineales con una activación ReLU entre ellas.  

6. **Normalización por Capas y Conexiones Residuales**  
   - **Propósito**: Estabilizar el entrenamiento y mejorar el flujo de gradientes al normalizar las entradas de cada capa y añadir conexiones de salto.  

## FastPitch
Con la teoría cubierta, examiné cada sección de la arquitectura de FastPitch en detalle. Ofrecí una breve explicación sobre las embeddings de palabras y la codificación posicional, ya que son temas complejos, y quise mantener la clase concisa.

FastPitch convierte texto en espectrogramas mel, que luego son transformados en audio por otro modelo (en nuestro caso, HiFi-GAN). La secuencia de entrenamiento incluye los siguientes pasos:

1. Texto a embeddings de palabras  
2. Concatenación de embeddings de palabras con espectrogramas mel  
3. Codificación posicional y FFT (bloque Transformer Feed-Forward)  
4. Predicción de tono  
5. Predicción de la duración de los fonemas  
6. Otro bloque FFT  
7. Capa completamente conectada  
8. Salida del espectrograma mel  

En cada bloque, presenté las ecuaciones correspondientes y proporcioné explicaciones cualitativas sobre su rol en el modelo. Por ejemplo, la predicción de la duración de los fonemas es crucial para alinear la duración de un fonema con la duración esperada en el espectrograma.

## Clase Online
Finalmente, resumí los puntos más importantes y realicé una clase online para compartir estos conceptos con mis colegas. Puedes verla aquí:

{{< youtube v4bt8bGIM00 >}}
