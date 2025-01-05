---
author: "Matías Di Bernardo"
title: "Understanding FastPitch and the Transformers Architecture"
date: "2023-08-23"
description: "A class I prepare to understand the TTS FastPitch model focusing on the Transformer architecture."
categories: [
    "Math",
    "Deep Learning",
]
tags: [
    "Work",
]
image: "front.png"
---

Understanding a modern deep learning model is challenging due to the extensive prior knowledge required and the rapid pace of advancements in the field. In the research project *Intercambios Transorgánicos*, we are working with TTS, specifically the FastPitch model from Nvidia. I have studied this model to fine-tune it for Spanish and shared my research process in a class to help my colleagues in the research group understand it better.

## Understanding Seq2Seq Models
In *Intercambios Transorgánicos*, we previously used Tacotron2 as our TTS model. While Tacotron2 performs well, it has several issues, primarily during training and inference, due to its auto-regressive nature. In contrast, FastPitch is a non-auto-regressive (NAR) model. To grasp these distinctions, I delved into seq2seq models, exploring their evolution over time and creating a quick overview of the sequence analysis models that have been pivotal:

- RNN
- LSTM
- Transformers

Tacotron2 is based on an LSTM (AR) model, whereas FastPitch utilizes Transformers (NAR). Understanding this technological progression provides crucial background knowledge, particularly about transformers, including positional encoding, a key factor in their non-auto-regressive nature, and the attention mechanism.

## The Transformer Architecture
I began by studying the transformer architecture, as it is fundamental to the FastPitch model. I reviewed online resources and the seminal *Attention is All You Need* paper. Below are some key points I noted during my study:

1. **Self-Attention Mechanism**  
   - **Purpose**: Dynamically focuses on different parts of the input sequence.  
   - **Mechanism**:  
     - Query (Q), Key (K), Value (V): Derived from input embeddings.  
     - Attention scores are computed as the dot product of Q and K, scaled by the square root of the dimension.  
     - Scores are normalized using softmax to create attention weights.  
     - A weighted sum of V is computed based on these weights to produce the output.  

2. **Multi-Head Attention**  
   - **Purpose**: Captures diverse relationships between tokens by applying multiple self-attention mechanisms in parallel.  
   - **Mechanism**: Outputs from multiple attention heads are concatenated and linearly transformed.  

3. **Positional Encoding**  
   - **Purpose**: Provides information about token order in the sequence, compensating for the Transformer's lack of built-in sequence order (unlike RNNs).  
   - **Mechanism**: A fixed or learnable vector is added to the input embeddings.  

4. **Encoder-Decoder Structure**  
   - **Encoder**: Processes the input sequence into context-rich representations.  
     - Components:  
       - Multi-head self-attention  
       - Feed-forward neural network (FFN)  
       - Layer normalization and residual connections  
   - **Decoder**: Generates the output sequence by attending to both encoder outputs and previously generated tokens.  
     - Components:  
       - Masked multi-head self-attention (prevents attending to future tokens)  
       - Multi-head attention over encoder outputs  
       - FFN, layer normalization, and residual connections  

5. **Feed-Forward Network (FFN)**  
   - **Purpose**: Introduces non-linearity and processes each token independently.  
   - **Mechanism**: Two linear layers with a ReLU activation in between.  

6. **Layer Normalization and Residual Connections**  
   - **Purpose**: Stabilizes training and improves gradient flow by normalizing inputs to each layer and adding skip connections.  

## FastPitch
After covering the theory, I examined each section of the FastPitch architecture in detail. I provided a brief explanation of word embeddings and positional encoding, as these are complex topics, and I wanted to keep the class concise.
FastPitch converts text into mel spectrograms, which are then transformed into audio by another model (in our case, HiFi-GAN). The training sequence involves the following steps:

1. Text to Word Embedding  
2. Word Embedding concatenated with mel spectrogram  
3. Positional encoding and FFT (Feed-Forward Transformer block)  
4. Pitch Prediction  
5. Phoneme Duration Prediction  
6. Another FFT block  
7. Fully connected layer  
8. Output mel spectrogram  

For each block, I presented the corresponding equations and provided qualitative explanations for their roles in the model. For instance, phoneme duration prediction is crucial for aligning a phoneme's duration with the expected duration in the spectrogram.

## Online Class
Finally, I summarized the most important points and conducted an online class to share these concepts with my colleagues. You can watch it here (in Spanish):

{{< youtube v4bt8bGIM00 >}}
