---
date: 2022-12-15 14:21:27
layout: post
title: "Reinforcement Learning : Deep Q Network"
subtitle:
description:
image: https://imgs.search.brave.com/Z6kkeMkj0SC8E6Udibi4czXFhFEoqB_JSBurnSdOPYM/rs:fit:1200:720:1/g:ce/aHR0cHM6Ly9pbWFn/ZXMubmludGVuZG9s/aWZlLmNvbS81NzU4/MTJmMDcxNGY5LzEy/ODB4NzIwLmpwZw
optimized_image:
category:
tags:
author:
paginate: false
---

This is the architecture of our Deep Q-Learning network:

![https://huggingface.co/blog/assets/78_deep_rl_dqn/deep-q-network.jpg](https://huggingface.co/blog/assets/78_deep_rl_dqn/deep-q-network.jpg)

As input, we take a **stack of 4 frames** passed through the network as a state and output a **vector of Q-values for each possible action at that state**. Then, like with Q-Learning, we just need to use our epsilon-greedy policy to select which action to take.

When the Neural Network is initialized, **the Q-value estimation is terrible**. But during training, our Deep Q-Network agent will associate a situation with appropriate action and **learn to play the game well**.

![https://huggingface.co/blog/assets/78_deep_rl_dqn/Q-target.jpg](https://huggingface.co/blog/assets/78_deep_rl_dqn/Q-target.jpg)