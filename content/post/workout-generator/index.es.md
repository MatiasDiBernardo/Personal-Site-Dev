---
author: "Matías Di Bernardo"
title: "Generador de ruitnas de entrenamiento automáticas"
date: "2022-06-22"
description: "Aplicación inteligante que genera rutinas de entrenamiento en base a datos ingresados por el usuario."
categories: [
    "Programming",
]
tags: [
    "University",
]
---

# Generador Automático de Rutinas de Ejercicio
Este proyecto fue el trabajo final para la asignatura Algoritmos y Programación II en la UNTREF. La idea de la aplicación es funcionar como una planificación inteligente de rutinas de ejercicio, donde el usuario ingresa ciertos criterios y el programa establece la mejor rutina para maximizar las preferencias del usuario. El programa fue escrito en el lenguaje de programación Go.

## Gestión de Datos
Este curso no se centra en bases de datos, por lo que optamos por usar un archivo CSV para simular una base de datos. Este archivo contiene toda la información sobre las diferentes rutinas y sus atributos. Esto sirve como un archivo de persistencia mientras que toda la lógica es manejada por el programa.

Los diferentes ejercicios están categorizados por temáticas. Hay dos entidades en el programa que están representadas como structs en Go: los Ejercicios y las Rutinas.

### Ejercicio
Todos los ejercicios tienen los siguientes atributos:

- Nombre: Nombre del ejercicio.
- Descripción: Descripción detallada del ejercicio.
- Duración: Duración estimada del ejercicio.
- Calorías: Número de calorías quemadas durante el ejercicio.
- Tipo: Tipo de ejercicio (por ejemplo, cardio, fuerza, flexibilidad).
- Grupo Muscular: Grupo muscular objetivo del ejercicio.
- Puntos: Puntos asignados al ejercicio según sus tipos.
- Dificultad: Nivel de dificultad del ejercicio.

### Rutinas
Todas las rutinas son una colección de ejercicios. Estas se procesan como una lista enlazada de ejercicios. Además, las rutinas tienen los siguientes atributos:
- Nombre: Nombre de la rutina.
- Ejercicios: Cadena que almacena los IDs de los ejercicios en la rutina, separados por comas.
- EjerciciosDisponibles: Lista enlazada de los ejercicios disponibles para crear la rutina.

## Algoritmo
La idea es maximizar diferentes parámetros, por ejemplo, la cantidad máxima de calorías quemadas en el menor tiempo posible, o la duración mínima para un grupo muscular o tipo de ejercicio específico. Para encontrar las mejores soluciones basadas en los datos existentes, proponemos un algoritmo de programación dinámica que busca todas las posibilidades a partir de los datos y encuentra el máximo o mínimo según las especificaciones del usuario. El enfoque de programación dinámica utiliza memoria para evitar recalcular combinaciones que ya fueron computadas, lo que optimiza el algoritmo lo suficiente como para generar las rutinas en milisegundos (con el conjunto de datos de prueba evaluado).

## Interfaz de Usuario
Actualmente, el programa está diseñado para ser utilizado desde la terminal como una aplicación CLI. El usuario puede crear un ejercicio y una rutina, listar las opciones disponibles y generar una rutina personalizada basada en las especificaciones que elija.

Esta es la primera iteración del proyecto y es completamente funcional, pero planeamos crear una interfaz gráfica para que sea más amigable para el usuario. Para este propósito, sería mejor usar un framework diferente y utilizar esta aplicación en Go como backend para un servicio web o una aplicación.

## Conclusiones
Con este proyecto, solidifiqué mis conocimientos sobre temas de programación como estructuras de datos y algoritmos, ya que aplicamos la teoría vista en clase a un caso real. También me ayudó a familiarizarme con el lenguaje Go, que se convirtió en un lenguaje que disfruto mucho programar. El código de este proyecto está disponible en este [repositorio](https://github.com/MatiasDiBernardo/Workout-routine-generator).
