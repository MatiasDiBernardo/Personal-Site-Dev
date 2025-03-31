---
author: "Matías Di Bernardo"
title: "Generative AI, Flow Matching and TTS"
date: "2025-03-24"
description: "A class I prepare to understand the model F5-TTS where I cover generative AI foundamentals and flow matching based models."
categories: [
    "Math",
    "Deep Learning",
]
tags: [
    "Work",
]
image: "front2.png"
---

At *Intercambios Transorgánicos*, we continuously work with state-of-the-art *Deep Learning* models. To achieve this, we stay up to date with the latest developments in the field. In this presentation, the objective was to explain the fundamentals of the *F5-TTS* model, a cutting-edge speech synthesis system. During the session, the concept of generative artificial intelligence and flow-based models was introduced, as *F5-TTS* is based on this technique. The purpose is to share this knowledge with the team and with anyone interested in getting started with *Text-to-Speech* (TTS) models.

## Introduction - Generative AI and TTS
The class was structured as follows:

1. **Introduction to TTS models**: Description of the different models used, their main characteristics, and the reasons behind changing approaches.
2. **Evolution of TTS models**: A graph-based survey illustrating the progression of various TTS technologies.
3. **Paradigm shift in language models**: Explanation of how using large datasets has enabled better generalization in language models.
4. **Example of generalization**: Illustrative cases, such as generating an image of an astronaut riding a horse, audio examples, and synthesis of specific accents (e.g., an angry Cordoban speaker).
5. **Change in dataset structuring**:
    - **Traditional approach**: Use of a single high-quality speaker with a large amount of data (model trained for each speaker).
    - **Current and future approach**: Use of diverse datasets with labels that enable training models capable of understanding speech concepts and generalizing across multiple tasks (*VoiceBox* examples).
    - **Computational cost**: Discussion of the increasing model size and training difficulty, similar to large-scale language models (*LLMs*).
6. **Explanation of Generative AI**:
    - Introduction to generative models and the concept of underlying distribution.
    - Explanation of *Transformers* and their function in classification with context. Clarification that while *Transformers* are *Non-Autoregressive* (NAR) during training, they operate *Autoregressively* (AR) in inference.
    - Difference between classification models and generative models based on dimensionality reduction and latent variables.

## TTS Models: VoiceBox, E2, and F5
This section details the key advancements in TTS models leading to the development of *F5-TTS*.

### 1. VoiceBox TTS - *In Context Learning*
The initial architecture of *VoiceBox* is introduced, focusing on generalization through *In Context Learning*. This approach allows the model to infer information based on prior examples. To achieve this, it is given an audio sample with a missing segment, forcing it to complete it coherently.

> *"We show that Voicebox’s text-guided speech infilling approach is much more scalable in terms of data while subsuming many common speech generative tasks."*

This method, introduced by Meta in *VoiceBox*, represents a paradigm shift by demonstrating that TTS models can benefit from techniques previously used in language and image models.

However, the model still relies on classical TTS techniques such as phoneme duration prediction and *Forced Alignment* to map phonemes to Mel spectrograms, as their lengths do not match those of text tokens.

### 2. E2 TTS - *Filler Tokens*
*E2 TTS* simplifies many of the architectural decisions of *VoiceBox*, particularly in handling the differing lengths of Mel spectrograms and text. Instead of using forced alignment, it introduces *Filler Tokens*, which allow text and audio dimensions to be equalized more efficiently. This approach makes it easier for the model to learn temporal associations between the two elements.

Another significant change is that the model directly processes text instead of phonemes. While this might seem disadvantageous (since homographic words can have different pronunciations), context provides enough information to infer the correct pronunciation, similar to how humans process natural language.

### 3. F5 TTS - *Open Source*
Although *E2 TTS* is a major step forward, its training is slow due to the need to infer associations that were previously guided. *F5 TTS* optimizes the previous model with the following improvements:

- **Use of ConvNeXt**: Enhances text processing.
- **Architectural change**: Replaces the *U-Net* network with *DiT* (*Diffusion Transformer*).
- **Sway Sampling**: Optimizes the inference process.

Additionally, *F5-TTS* is open-source, facilitating adoption and improvement by the community.

## Flow Matching - Theoretical Foundations
To understand how *F5-TTS* works, it is essential to review the models it is based on, known as *Flow Matching Models*. These models have evolved from previous techniques in probabilistic distribution modeling.

### 1. Normalizing Flow
*Normalizing Flows* are a family of probabilistic models that transform a simple distribution into a more complex one through a series of invertible and differentiable functions. They are used to model high-dimensional data distributions and generate realistic samples with precise control over probability.

### 2. Residual Flow
*Residual Flows* extend *Normalizing Flows* by allowing more flexible transformations without strictly adhering to the invertibility condition. This is achieved through residual networks that approximate transformation functions without structural constraints.

### 3. Continuous Normalizing Flows (CNF)
*Continuous Normalizing Flows* reformulate *Normalizing Flows* using ordinary differential equations (ODEs). Instead of applying discrete transformations in successive steps, these models learn a continuous dynamic in the latent space, allowing for greater expressiveness and computational efficiency.

### 4. Flow Matching
*Flow Matching* is a technique that optimizes the transformation of a reference distribution into a target distribution by minimizing a specific cost function. It differs from previous approaches by not requiring explicit density function calculations, making it particularly useful for large-scale generative models such as *F5-TTS*.

## Online Presentation
All of this sections are explained in detail on the online class avaliable here (in Spanish):

{{< youtube YIpvFC41NUw >}}