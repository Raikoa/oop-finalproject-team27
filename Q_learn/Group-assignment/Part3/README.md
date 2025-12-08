# OOP Final Project: Multi-Agent Warehouse RL Environment (Part 3)

## Project Overview

This repository contains Part 3 of the OOP Final Project. It implements a custom, two-agent Warehouse Environment based on Reinforcement Learning (RL).
The environment is built using the Gymnasium library’s `Env` class, providing a standardized interface for RL training.

The project uses the Proximal Policy Optimization (PPO) algorithm from the Stable-Baselines3 library to train an RL model capable of controlling two agents simultaneously.

### Goal of the Environment

The primary objective of the environment is for two agents to cooperatively deliver four packages from their spawning locations to a designated offloading area.

---

## Dependencies

The following packages are required:

- gymnasium
- numpy
- random
- os
- stable-baselines3
- pygame

Install using:

    pip install gymnasium numpy stable-baselines3 pygame

---

## How to Run the Trained Model

Follow the steps below to load the pre-trained PPO model and visualize the agents in the custom `WareHouseEnv`.

### 1. Run the imports and classes and helper functions

Ensure you have all necessary imports and the `WareHouseEnv`, `Agent`,  `package` and its subclasses, `ExpressPackage` and `HeavyPackage`, as well as the helper function `manhatton` defined in your script.

### 2. Load the PPO Model

Update the file path as needed for your system:

    model = PPO.load(
        r"C:\Users\Brian\Downloads\warehouse\Q_learn\Training\Saved Models\WareHouse_Model_multi_ver3_PPO.zip",
        env=env
    )

### 3. Initialize the Environment and Pygame

    env = WareHouseEnv()
    env.init_pygame()

### 4. Run the Simulation Loop

The following script runs five episodes, renders the environment, and prints episode scores:

    import time
    import os

    episodes = 5
    for episode in range(1, episodes + 1):
        obs, info = env.reset()
        done = False
        score = 0

        while not done:
            # Clear console for animation effect
            os.system("cls" if os.name == "nt" else "clear")

            env.render()  # Render current environment state

            action, _ = model.predict(obs, deterministic=True)
            obs, reward, terminated, truncated, info = env.step(action)

            done = terminated or truncated
            score += reward

            time.sleep(0.05)  # Slow rendering speed for visibility

        print(f"Episode {episode} Score {score}")

    env.close()

---


contribution:
B124020010

