# OOP Final Project: Multi-Agent Warehouse RL Environment (Part 3)

## Project Overview

This repository contains **Part 3** of the OOP Final Project. It implements a custom, two-agent **Warehouse Environment** based on the principles of Reinforcement Learning (RL).

The environment is built using the **Gymnasium** (formerly Gym) library's `Env` class, providing a standardized interface for RL training.

The project uses the **Proximal Policy Optimization (PPO)** algorithm from the **Stable Baselines3** library to train an RL model capable of controlling the agents.

### Goal of the Environment

The primary objective of the two agents within the warehouse environment is to successfully **deliver 4 packages** from their spawning locations to the designated **offloading area**.

## Dependencies

The following packages are required to run the environment and utilize the trained model:

* `gymnasium` (The core environment interface)
* `numpy` (Numerical operations)
* `random` (For environment dynamics)
* `os` (Operating system interaction for rendering)
* `stable_baselines3` (RL algorithms and model loading)
* `pygame` (For visual rendering of the environment)

You can typically install these using `pip`:


pip install gymnasium numpy stable-baselines3 pygame


How to Run the Trained Model
Follow these steps to load the pre-trained PPO model and visualize the two agents' performance in the custom WareHouseEnv.
1. run the imports at the top  
2. Load the Model
Initialize and load the trained PPO model. NOTE: You must ensure the file path is correct for your system.
model = PPO.load(r"C:\Users\Brian\Downloads\warehouse\Q_learn\Training\Saved Models\WareHouse_Model_multi_ver3_PPO.zip", env=env)
3.Initialize the Environment and Pygame
Create an instance of the custom environment and set up the Pygame rendering window:
env = WareHouseEnv()
env.init_pygame()
4.Run the Simulation Loop
Execute the following script to run 5 episodes, visualize the agents' actions, and print the resulting score:

import time
import os

episodes = 5
for episode in range(1, episodes + 1):
    obs, info = env.reset()
    done = False
    score = 0

    while not done:
        # Clear console (optional, makes the render look like animation)
        os.system("cls" if os.name == "nt" else "clear")

        env.render()       # <-- Render the current state

        action, _ = model.predict(obs, deterministic=True)
        obs, reward, terminated, truncated, info = env.step(action)

        done = terminated or truncated
        score += reward

        time.sleep(0.05)   # Slow down for visibility (adjust as needed)

    print(f"Episode {episode} Score {score}")

env.close()


contribution:
B124020010

