---
author: "Matías Di Bernardo"
title: "IA aprende a jugar 2048"
date: "2023-02-17"
description: "Aplique *reinforcement learning* para hacer que un agente aprenda a jugar el juego 2048 usano Q-Learning y redes neuronales."
categories: [
    "Programming",
    "Deep Learning",
]
tags: [
    "Personal Project",
]
image: "game_img.jpg"
math: true
---
Usé este proyecto como introducción al Aprendizaje por Refuerzo (Reinforcement Learning). Habiendo trabajado principalmente con aprendizaje supervisado y no supervisado, quería comenzar con un proyecto pequeño y sencillo para comprender rápidamente las ideas principales y crear algo divertido. Seguí este [video de YouTube](https://youtu.be/L8ypSXwyBds) como referencia, el cual explica cómo usar Aprendizaje por Refuerzo (RL) para entrenar un modelo capaz de jugar al juego de la serpiente. Para hacerlo más desafiante, apliqué la misma red al juego 2048.

## Código
El código tiene tres componentes principales:
- **El Juego**: Implementa la lógica del juego y la interfaz gráfica (GUI).
- **Agente**: Controla la jugabilidad.
- **Modelo de IA**: Una red neuronal que aprende a jugar y guía al agente.

### Estado del Juego
Modelé el estado del juego como una matriz de 4x4 que representa el tablero. Las acciones del juego están representadas por un vector con las siguientes posibilidades:

- **Izquierda**: [1, 0, 0, 0]  
- **Derecha**: [0, 1, 0, 0]  
- **Arriba**: [0, 0, 1, 0]  
- **Abajo**: [0, 0, 0, 1]  

### Recompensa
El modelo de RL funciona con recompensas para cuantificar cuándo el agente actúa bien o mal. Inicialmente, definí las siguientes recompensas:
- **+10 puntos**: Cuando el agente duplica los puntos. Esto es crucial porque, en 2048, los puntos aumentan exponencialmente.
- **-10 puntos**: Cuando se pierde el juego. Esto sirve como una penalización sencilla.

Al principio, el modelo mostraba una mejora lenta. Para solucionarlo, añadí una recompensa adicional:
- **+2 puntos**: Cuando se incrementan los puntos. Esta recompensa incentiva acciones que maximicen la limpieza del tablero y el progreso.

## Cómo Funciona el Modelo
El modelo es una red neuronal lineal simple. Toma el estado del juego como entrada y predice la mejor acción siguiente para maximizar la recompensa.

Las recompensas se gestionan utilizando una técnica llamada Q-Learning. Un *valor Q* representa la calidad de una decisión basada en la función de pérdida. La función de pérdida se deriva de la *Ecuación de Bellman*:

$$
NewQ(s, a) = Q(s, a) + \alpha [R(s, a) + \lambda \, \text{max}Q'(s', a') - Q(s, a)]
$$

Donde:
- $Q(s, a)$: El *valor Q* para un estado y acción específicos.  
- $\alpha$: Tasa de aprendizaje.  
- $R(s, a)$: Recompensa para un estado y acción específicos.  
- $\lambda$: Tasa de descuento.  
- $\text{max}Q'(s', a')$: Recompensa futura máxima esperada.  

## Experimentos y Resultados
### Prueba Aleatoria como Línea Base
Para establecer una línea base, probé el puntaje promedio que se puede lograr tomando acciones aleatorias. Después de 1,000 iteraciones, el puntaje promedio fue de **170**, muy por debajo de los 2048 puntos necesarios para ganar el juego.

### Resultados Iniciales
Mis primeros intentos fueron desalentadores. El modelo tenía un desempeño peor que los movimientos aleatorios. Aquí algunos resultados iniciales:
1. **Juego 1,000** | Puntaje: 208 | Récord: 416 | Puntaje Promedio: 200 | Recompensa: 640  
2. **Juego 1,000** | Puntaje: 116 | Récord: 346 | Puntaje Promedio: 161 | Recompensa: 310  
3. **Juego 1,000** | Puntaje: 112 | Récord: 348 | Puntaje Promedio: 146 | Recompensa: 320  

En estos intentos, el agente desarrolló una estrategia subóptima de llenar el tablero antes de incrementar los puntos.

### Mejoras
Tras experimentar con los parámetros de recompensa, me centré en la fase de exploración. Inicialmente, el parámetro de *juegos de exploración*, que elige movimientos aleatorios, estaba configurado en 25 juegos. Al aumentar este parámetro, el agente pudo explorar más estrategias, logrando mejores resultados:

4. **Juego 1,000** | Puntaje: 478 | Récord: 478 | Puntaje Promedio: 230  
5. **Juego 1,000** | Puntaje: 514 | Récord: 964 | Puntaje Promedio: 382  

A medida que el modelo mejoraba, extendí el entrenamiento a más juegos:

6. **Juego 3,796** | Puntaje: 770 | Récord: 1,366 | Puntaje Promedio: 469  
7. **Juego 4,852** | Puntaje: 631 | Récord: 1,462 | Puntaje Promedio: 483  

Finalmente, con 200 juegos de exploración y 5,000 juegos de entrenamiento, los resultados fueron los siguientes:

8. **Juego 5,000** | Puntaje: 840 | Récord: 1,678 | Puntaje Promedio: 512  

Aunque el modelo no logró ganar el juego, quedé satisfecho con el progreso. Creo que con más tiempo de entrenamiento (el último intento duró 4 horas) y capas adicionales en la red, sería posible ganar el juego con esta arquitectura.

## Demo
Aquí tienes una demostración de la aplicación, mostrando el proceso de aprendizaje del agente:

{{< vimeo 1045495533 >}}

Implementé atajos de teclado para controlar la velocidad del juego, ofreciendo tres opciones:
- **Rápida**: Para un entrenamiento acelerado.  
- **Lenta**: Para observar y analizar el progreso del agente y sus errores.  
- **Media**: Casi no la utilicé.  

El código completo para este proyecto está disponible en este [repositorio](https://github.com/MatiasDiBernardo/RF_2048-game).
