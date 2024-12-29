---
author: "Matías Di Bernardo"
title: "Time Scale Modification Algorithms"
date: "2023-02-11"
description: "Developement and evaluation of different TSM algorithms with python."
categories: [
    "DSP",
    "Programming",
]
tags: [
    "Academic",
    "University",
]
image: "tsm.PNG"
---

# Time Scale Modification (TSM)
Time scale modifications algorithms are used to speed up or slow down the reproduction velocity of an audio. When you change the sample rate of an audio, the velocity changes but it also changes the pitch (when the audio is speed up it sounds highier pitch). There are different algorithms that change the velocity of the audio but mantain the pitch.

The main reference for this study is the following article, where all the different algorithms are describe in detail.

> A Review of Time-Scale Modification of Music Signals.<br>
> — <cite>Jonathan Driedger and Meinard Müller[^1]</cite>

[^1]: A Review of Time-Scale Modification of Music Signal [paper](https://www.researchgate.net/publication/295082364_A_Review_of_Time-Scale_Modification_of_Music_Signals).

## Algorithm comparison
There are two main algorithms, the *Overlap-and-add* (OLA) and the *Phase Vocoder* (PV). Both achieve good results under different signals and conditions. For this, a final implementation using *Harmonic Percussion Separation* (HPS) combines both algorithms and achiving the best results.

### OLA
This method works on time domain and overlap sections of the audio (windows) and rearange it to achive a certain desire change on speed. This method works well for percussive signals, but it introduces artifacts when used with harmonic or tonal signals.

### PV
This method works on frequency domain, and it combines chunks of audio in the frequency domain to achieve the desire change in time. This uses the phase vocoder principle to propagate the phase between the windows, this grantice the continuity of when applied to harmonic signals. On the contrary, it does not work for percussive signals becouse the phase propagation process eliminate the transients in the signals.  

### HPS 
To use both methods with their ideal signals, the HPS algorithms is used. This algorithm separete the signal into the harmonics and the percussive parts. It works by comparing the continuty of the signal in the STFT representation and using a filter to compare vertical versus horizontal presence on the spectrogram. With a threshold, a binary mask can be define over the spectrogram to separete the percussive parts from the harmoincs sections.

## Results
We succesfully implement all the algorithms and compare them, verifying the theortical contents presented on the referenca article. In the process, we develope the toolkit to use this algorithms with the python programming language. All the code is avaliable on this [repo](https://github.com/MatiasDiBernardo/TSM_Toolkit)

## Academic Presentation
The study was preseented with my classmates on the *JAAS* (Jornadas de Acustica, Audio y Sonido). The main ideas and conclusions were preseneted on the conference. In the following repoert there is all the details and anlysis done for this proyect (in spanish).

> ALGORITMOS DE MODIFICACIÓN DE ESCALA TEMPORAL.<br>
> — <cite>Matías Di Bernardo; Matías Vereertbruhggen; Sebastían Carro [^2]</cite>


[^2]: JAAS 2023 - Algoritmos de Modificación de Escala Temporal [paper](https://drive.google.com/file/d/12kPB3qBjczyx7X2XV3ZpBDo1GDO2u4qR/view?usp=sharing).
