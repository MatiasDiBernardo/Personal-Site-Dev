---
author: "Matías Di Bernardo"
title: "The effect of denosing on TTS"
date: "2024-11-22"
description: "Subjective study to understand the effect of denoising on TTS and to compare different state-of-the-art denoising algorithms."
categories: [
    "Acoustics",
    "Deep Learning",
]
tags: [
    "Academic",
]
---

This study was conducted in the context of the class *Laboratorio de Acústica* at UNTREF. I chose this topic because it aligns with research I have been pursuing as part of the group *Intercambios Transorgánicos*. The class assignment involved conducting a subjective study using a survey to explore the relationship between objective and subjective variables.

In my research group, I have been investigating how denoising algorithms affect Text-to-Speech (TTS) systems trained on low-quality recordings. The focus is on Rioplatense Spanish, a regional accent with limited high-quality data. Within this context, it was natural to combine both tasks and perform a subjective test on the impact of denoising algorithms on TTS systems.

## Overview
The key points of this investigation are:
- Evaluation of three denoising algorithms: Wave U-Net, HiFi-GAN, and DeepFilterNet.
- Use of both subjective (CMOS) and objective metrics (PESQ, STOI, MCD).
- Insights into resource-efficient TTS model development for underrepresented accents.

## Methodology
- **Algorithms**: Wave U-Net, HiFi-GAN, and DeepFilterNet evaluated with the FastPitch TTS model.
- **Dataset**: Subset of the ArchiVoz collection (15 minutes of noisy audio).
- **Testing**: CMOS subjective test and objective metrics (PESQ, STOI, MCD).
- **Participants**: 24 valid responses, including both experts and non-experts.

## Key Findings
1. **DeepFilterNet Performance**:
   - Achieved the highest CMOS score, reflecting the best subjective quality.
   - Demonstrated significant improvements in TTS output despite mixed correlations with objective metrics.

2. **Objective Metrics Analysis**:
   - PESQ and MCD showed limited correlation with subjective preferences.
   - STOI scores were consistent across algorithms, indicating preserved intelligibility.

3. **Algorithm Comparisons**:
   - **DeepFilterNet**: Superior subjective evaluations, moderate MCD.
   - **Demucs**: Comparable to DeepFilterNet in PESQ but lower subjective scores.
   - **Wave U-Net**: Poor subjective and objective performance.

4. **Subject Expertise**:
   - No significant differences were observed between expert and non-expert evaluations in subjective testing.

## Implications
- **Efficiency**: Advanced denoising methods like DeepFilterNet can enhance TTS systems without requiring high-quality recordings.
- **Limitations**: Objective metrics like PESQ and MCD are insufficient standalone indicators of subjective TTS quality.
- **Future Work**:
  - Expand datasets and noise levels for more robust analysis.
  - Explore TTS systems trained jointly with denoising algorithms.

## Conclusions
This work concludes that preprocessing with DeepFilterNet significantly improves TTS performance, with a 1.1 CMOS score increase. These findings underscore the importance of algorithm selection in optimizing low-resource TTS systems. Additionally, I gained valuable insights into subjective evaluations and the statistical analysis required to draw meaningful conclusions from data.

All the information for this study can be found in the [academic report](https://drive.google.com/file/d/1F4aJGIU9FX2LT8OFik-Yjg4uSz6T09jw/view?usp=sharing).
