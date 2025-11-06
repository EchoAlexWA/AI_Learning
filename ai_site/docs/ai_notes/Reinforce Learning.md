# Reinforce Learning
## Overview
Reinforcement Learning (RL) is a type of machine learning where an agent learns to make decisions by taking actions in an environment to maximize cumulative rewards. Unlike supervised learning, where the model learns from labeled data, RL relies on feedback from the environment in the form of rewards or penalties.

Essential elements of Reinforcement Learning include:

- **Policy**: A strategy used by the agent to determine the next action based on the current state.
$$
\pi(a|s) = P(A_t = a | S_t = s)
$$

- **Reward Function**: A function that provides feedback to the agent based on the action taken.
$$
R_t = R(S_t, A_t, S_{t+1})
$$
Cumulative reward is often calculated using a discount factor \( \gamma \):
$$
G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}
$$

- **Value Function**: A function that estimates the expected cumulative reward from a given state or state-action pair.
$$
V^{\pi}(s) = \mathbb{E}_{\pi} \left[ G_t | S_t = s \right] = \mathbb{E}_{\pi} \left[ \sum_{k=0}^{\infty} \gamma^k R_{t+k+1} | S_t = s \right]
$$
Value of taking action a in state s under policy $\pi$:
$$
Q^{\pi}(s, a) = \mathbb{E}_{\pi} \left[ G_t | S_t = s, A_t = a \right]
$$
The relationship between state-value and action-value functions:
$$
V^{\pi}(s) = \sum_{a} \pi(a|s) Q^{\pi}(s, a)
$$


- **Model of the Environment**: An optional component that predicts the next state and reward given the current state and action.
$$
P(S_{t+1}, R_{t+1} | S_t, A_t)
$$