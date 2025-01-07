---
author: "Matías Di Bernardo"
title: "Evaluation of different models for Speaker Diarization task"
date: "2022-11-04"
description: "Implement from scratch a Speaker Diarization model with SNN and comapre it to other implementations."
categories: [
    "Deep Learning",
]
tags: [
    "Personal Project",
]
---

This project started as the final assignment for a seminar class at UNTREF called *Seminario en Aplicaciones de Redes Neuronales en la recuperación de información musical*. The objective was to use a Siamese Neural Network (SNN) in a different context than the one explored in class (music similarity detection).

For the final project of this course, we developed an SNN model from scratch using the *Keras* framework and the *SincNet* architecture to reduce audio dimensionality, achieving good results. Later, to expand this project, I tried another approach by using *Wav2Vec* for dimensionality reduction and re-implementing the entire project in the *PyTorch* framework. This attempt, however, yielded suboptimal results, indicating that the dimensionality reduction using Wav2Vec lost critical information required for the speaker diarization task.

## Speaker Diarization Task
The goal of a speaker diarization model is to identify different speakers in an audio stream containing multiple speakers. For example, in a podcast with two people (A and B), the model must determine the time steps where speaker A is talking and the time steps where speaker B is speaking (and implicitly identify the periods of silence). These models are incredibly useful for audio editing and analyzing long audio sequences with multiple speakers.

## Why Siamese Neural Networks?
In class, we explored the Siamese architecture to compare similarities between pieces of music, developing a tool capable of identifying covers of famous songs.

A Siamese Neural Network consists of two or more identical subnetworks sharing the same weights and parameters. It is designed to compare input pairs and measure their similarity, typically using a distance metric like Euclidean distance. Each subnetwork processes one input, and the outputs are combined to compute a similarity score.

With this similarity comparison in mind, we wanted to apply these networks to the speaker diarization task. The idea was to generate speaker embeddings from audio using a pre-trained model and compare the outputs of different audio segments. Based on the similarity score, we aimed to identify the segments where different speakers are talking.

## Experiments
I tested two different methods for audio feature extraction to serve as speaker embeddings.

### Keras Implementation with SincNet
In this approach, we used the SincNet architecture to extract speaker-specific features from audio. SincNet applies learnable sinc functions as its filters, which are particularly well-suited for audio processing as they mimic traditional bandpass filters. These features were then fed into the Siamese Neural Network, which compared pairs of audio segments to calculate their similarity scores. The model was trained on labeled audio datasets, and we observed strong performance in clustering audio segments by speaker, achieving clear boundaries between different speakers.

A report with the results can be found in the following [Jupyter notebook](https://github.com/MatiasDiBernardo/Speaker-Diarization-with-SNN/blob/master/TP%20Final%20Seminario%20Redes%20-%20Di%20Bernardo%20Ferreyra.ipynb) (in Spanish).

### PyTorch Implementation with Wav2Vec
For this method, I utilized Wav2Vec, a powerful pre-trained model for extracting deep audio embeddings. Unlike SincNet, Wav2Vec embeddings are derived from self-supervised learning, capturing high-level representations of audio. These embeddings were used in the Siamese Neural Network for similarity comparisons. However, the results were suboptimal for the diarization task. It appears that Wav2Vec, while excellent for speech recognition tasks, lost some speaker-specific details necessary for distinguishing between speakers in our setup.

## Results
The experiments demonstrated that the choice of feature extraction method is crucial for speaker diarization. The Keras implementation with SincNet outperformed the PyTorch implementation with Wav2Vec, showing higher accuracy in identifying speaker transitions. This suggests that task-specific feature extraction, like SincNet, is more effective than general-purpose embeddings like Wav2Vec for speaker diarization.

The code for this project is available in this [repository](https://github.com/MatiasDiBernardo/Speaker-Diarization-with-SNN).

## Conclusions
This project was one of my first experiences with deep learning models, where I applied my knowledge to a problem without following a specific paper or using a pre-trained model. I explored different solutions and concluded on the importance of feature extraction and model selection.

It also helped me become familiar with the syntax of the most popular deep learning frameworks and solidified my understanding in the process.
