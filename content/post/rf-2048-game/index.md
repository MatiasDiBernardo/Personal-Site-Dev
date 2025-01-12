---
author: "Matías Di Bernardo"
title: "AI learns to play 2048 game"
date: "2023-02-17"
description: "Used reinforcement learning to train an agent to be able to play the game 2048 using Q-learning and neuronal networks."
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

I used this project as an introduction to Reinforcement Learning. Having mostly worked with supervised and unsupervised learning, I wanted to start with a small, simple project to quickly grasp the main ideas and create something fun. I followed this [YouTube video](https://youtu.be/L8ypSXwyBds) as a reference, which explains how to use Reinforcement Learning (RL) to train a model capable of playing the snake game. To make it more challenging, I applied the same network to the 2048 game.

## Code
The code has three main components:
- **The Game**: Implements the game logic and the graphical user interface (GUI).
- **Agent**: Controls the gameplay.
- **AI Model**: A neural network that learns how to play and guides the agent.

### Game State
I modeled the game state as a 4x4 matrix representing the board. The actions in the game are represented by a vector, with the following possibilities:

- **Left**: [1, 0, 0, 0]
- **Right**: [0, 1, 0, 0]
- **Up**: [0, 0, 1, 0]
- **Down**: [0, 0, 0, 1]

### Reward
The RL model works with rewards to quantify when the agent performs well or poorly. Initially, I defined the following rewards:
- **+10 points**: When the agent doubles the points. This is crucial because, in 2048, points increase exponentially.
- **-10 points**: When the game is lost. This serves as a straightforward negative reward.

Initially, the model showed slow improvement. To address this, I added an additional reward:
- **+2 points**: When points are increased. This reward incentivizes actions that maximize board clearance and progress.

## How the Model Works
The model is a simple linear neural network. It takes the game state as input and predicts the best next action to maximize the reward.

Rewards are managed using a technique called Q-Learning. A *Q Value* represents the quality of a decision based on the loss function. The loss function is derived from the *Bellman Equation*:

$$
NewQ(s, a) = Q(s, a) + \alpha [R(s, a) + \lambda \, \text{max}Q'(s', a') - Q(s, a)]
$$

Where:
- $Q(s, a)$: The *Q Value* for a specific state and action.
- $\alpha$: Learning rate.
- $R(s, a)$: Reward for a specific state and action.
- $\lambda$: Discount rate.
- $\text{max}Q'(s', a')$: Maximum expected future reward.

## Experiments and Results
### Random Test as a Baseline
To establish a baseline, I tested the average score achievable by taking random actions. After 1,000 iterations, the average score was **170**, far below the 2048 points needed to win the game.

### Initial Results
My initial attempts were discouraging. The model performed worse than random movements. Here are some early results:
1. **Game 1,000** | Score: 208 | Record: 416 | Mean Score: 200 | Reward: 640  
2. **Game 1,000** | Score: 116 | Record: 346 | Mean Score: 161 | Reward: 310  
3. **Game 1,000** | Score: 112 | Record: 348 | Mean Score: 146 | Reward: 320  

In these attempts, the agent developed a suboptimal strategy of filling the board before increasing points.

### Improvements
After experimenting with the reward parameters, I focused on the exploration phase. Initially, the *exploration games* parameter, which randomly picks moves, was set to 25 games. Increasing this parameter allowed the agent to explore more strategies, leading to better results:

4. **Game 1,000** | Score: 478 | Record: 478 | Mean Score: 230  
5. **Game 1,000** | Score: 514 | Record: 964 | Mean Score: 382  

As the model improved, I extended the training to more games:

6. **Game 3,796** | Score: 770 | Record: 1,366 | Mean Score: 469  
7. **Game 4,852** | Score: 631 | Record: 1,462 | Mean Score: 483  

Finally, with 200 exploration games and 5,000 training games, the results were as follows:

8. **Game 5,000** | Score: 840 | Record: 1,678 | Mean Score: 512  

Although the model didn't beat the game, I was satisfied with the progress. I believe that with longer training (the final run lasted 4 hours) and additional network layers, it would be possible to win the game using this architecture.

## Demo
Here is a demo of the application, showcasing the agent's learning process:

{{< vimeo 1045495533 >}}

I implemented keybindings to control the game's speed, providing three options:
- **Fast**: For rapid training.
- **Slow**: To observe and analyze the agent's progress and mistakes.
- **Medium**: Rarely used.

The complete code for this project is available in this [repository](https://github.com/MatiasDiBernardo/RF_2048-game).
