---
author: "Matías Di Bernardo"
title: "Automatic Workout Routine Generator"
date: "2023-04-17"
description: "Smart application that defines a workout routine based on input parameters."
categories: [
    "Programming",
]
tags: [
    "University",
]
---

# Automatic Workout Routine Generator
This project was the final project asignment for the Algoritmos y Programación II on UNTREF. The idea of the application is to function as a smart workout planification, where the user input certain criterias and the program establish the best workout routine to maximice the users preference. The program was written in the Go programming language.

## Data Management
This course does not focues on databases, so we choose to use a CSV to simulate a database. This file contains all the information of the different routines and the differente attributes. This serve as a presistency file wheras all the logic is handle by the program.

Different exercises are categorized by tematics. There are two entities on the program that are represented as structs in Go, this are the Exercise and the Routines.

### Exercise
All the exercises have the following attributes:

- Name: Name of the exercise.
- Description: Detailed description of the exercise.
- Duration: Estimated duration of the exercise.
- Calories: Number of calories burned during the exercise.
- Type: Type of exercise (e.g., cardio, strength, flexibility).
- Muscle Group: Muscle group targeted by the exercise.
- Points: Points assigned to the exercise for each of its types.
- Difficulty: Difficulty level of the exercise.

### Routines
All the routines are a collection of exercises. This are paresed as a linked list of exercise. Aside from this, the routins have the following attributes:
- Name: Name of the routine.
- Exercises: String that stores the IDs of the exercises in the routine, separated by commas.
- AvailableExercises: Linked list of the exercises available for creating the routine.

## Algorithm
The idea is to maximice different parameters, for example, maximum calories burnt in the least ammount of time, or the minimum duration for this muscle group or type of exercise. To find the best solutions based on the existing data we propose a dynamic programming algorithm that searches for all the posiblities from the data and find the maximum or minimum according to the specifications of the user. The DP apprach uses memory to avoid recalculation combinantions that already were computed, with this optimization the algorithm is fast enough that can generate the routines in miliseconds (with the test dataset under evaluation).

## User Interface
At the moment, the programm is designed to be used form the terminal as a CLI application. The user can crear an exersice and a rutine, list the avaliable optionas, and generate a custom routine base on the specifications that he choose.

This is the first iteration of the project and it is fully functional but we plan to create a custom GUI to be user friendly, but for this proposse it will be better to use a different framework and use this GO application as the backend for a web or app service.

## Conclusions
With this project I solidify my knowledege on programming topics like data structurs and algorithms because we used the theory seen in class and applied it to a real case scenario. Also it help me to get used to the Go langeage and it became a leangauge that I really enjoy coding on it. The code for this project is avaliable on this [repository](https://github.com/MatiasDiBernardo/Workout-routine-generator).
