---
author: "Matías Di Bernardo"
title: "Efecto de algorítmos de reducción de rudio en sistemas de TTS"
date: "2024-11-22"
description: "Evaluación subjetiva de la preferencia y naturalidad de sistemas TTS entrenados con diferentes algoritmos de denoising."
categories: [
    "Acoustics",
    "Deep Learning",
]
tags: [
    "Academic",
]
---

Este estudio se realizó en el contexto de la clase *Laboratorio de Acústica* en la UNTREF. Elegí este tema porque está alineado con investigaciones que he estado desarrollando como parte del grupo *Intercambios Transorgánicos*. La consigna para el trabajo de clase consistió en realizar un estudio subjetivo utilizando una encuesta para explorar la relación entre variables objetivas y subjetivas.

En mi grupo de investigación, he estado investigando cómo los algoritmos de reducción de ruido afectan a los sistemas de síntesis de voz (TTS) entrenados con grabaciones de baja calidad. El enfoque está en el español rioplatense, un acento regional con datos de alta calidad limitados. En este contexto, fue natural combinar ambas tareas y realizar una prueba subjetiva sobre el impacto de los algoritmos de reducción de ruido en los sistemas TTS.

## Resumen
Los puntos clave de esta investigación son:
- Evaluación de tres algoritmos de reducción de ruido: Wave U-Net, HiFi-GAN y DeepFilterNet.
- Uso de métricas subjetivas (CMOS) y objetivas (PESQ, STOI, MCD).
- Ideas sobre el desarrollo de modelos TTS eficientes en recursos para acentos poco representados.

## Metodología
- **Algoritmos**: Wave U-Net, HiFi-GAN y DeepFilterNet evaluados con el modelo TTS FastPitch.
- **Conjunto de datos**: Subconjunto de la colección ArchiVoz (15 minutos de audio con ruido).
- **Pruebas**: Prueba subjetiva CMOS y métricas objetivas (PESQ, STOI, MCD).
- **Participantes**: 24 respuestas válidas, incluyendo tanto expertos como no expertos.

## Principales Hallazgos
1. **Rendimiento de DeepFilterNet**:
   - Obtuvo la puntuación CMOS más alta, reflejando la mejor calidad subjetiva.
   - Mostró mejoras significativas en la salida TTS a pesar de las correlaciones mixtas con las métricas objetivas.

2. **Análisis de Métricas Objetivas**:
   - PESQ y MCD mostraron una correlación limitada con las preferencias subjetivas.
   - Las puntuaciones STOI fueron consistentes entre los algoritmos, indicando inteligibilidad preservada.

3. **Comparación de Algoritmos**:
   - **DeepFilterNet**: Evaluaciones subjetivas superiores, MCD moderado.
   - **Demucs**: Comparable a DeepFilterNet en PESQ, pero con puntuaciones subjetivas inferiores.
   - **Wave U-Net**: Bajo rendimiento tanto subjetivo como objetivo.

4. **Experiencia de los Participantes**:
   - No se observaron diferencias significativas entre las evaluaciones subjetivas de expertos y no expertos.

## Implicaciones
- **Eficiencia**: Métodos avanzados de reducción de ruido como DeepFilterNet pueden mejorar los sistemas TTS sin necesidad de grabaciones de alta calidad.
- **Limitaciones**: Las métricas objetivas como PESQ y MCD no son indicadores suficientes por sí solas de la calidad subjetiva en TTS.
- **Trabajo Futuro**:
  - Ampliar los conjuntos de datos y niveles de ruido para un análisis más robusto.
  - Explorar sistemas TTS entrenados conjuntamente con algoritmos de reducción de ruido.

## Conclusiones
Este trabajo concluye que el preprocesamiento con DeepFilterNet mejora significativamente el rendimiento de los sistemas TTS, con un aumento de 1.1 en la puntuación CMOS. Estos hallazgos destacan la importancia de la selección de algoritmos para optimizar sistemas TTS con pocos recursos. Además, adquirí valiosos conocimientos sobre evaluaciones subjetivas y el análisis estadístico necesario para extraer conclusiones significativas de los datos.

Toda la información de este estudio se encuentra en el [informe académico](https://drive.google.com/file/d/1F4aJGIU9FX2LT8OFik-Yjg4uSz6T09jw/view?usp=sharing) (en inglés).
