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
Cumulative reward is often calculated using a discount factor \( \gamma\in [0, 1) \):
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

## Bellman Equations
The Bellman equations provide a recursive decomposition for the value functions:
- For the state-value function:
$$
\begin{aligned}
V^{\pi}(s) = \mathbb{E}_{\pi} \left[ R_t + \gamma V^{\pi}(S_{t+1}) | S_t = s \right]\\
= \sum_{a} \pi(a|s) \sum_{s', r} P(s', r | s, a) \left[ r + \gamma V^{\pi}(s') \right]
\end{aligned}
$$
- For the action-value function:
$$
\begin{aligned}
Q^{\pi}(s, a) = \mathbb{E}_{\pi} \left[ R_t + \gamma V^{\pi}(S_{t+1}) | S_t = s, A_t = a \right]\\
= \sum_{s', r} P(s', r | s, a) \left[ r + \gamma \sum_{a'} \pi(a'|s') Q^{\pi}(s', a') \right]
\end{aligned}
$$

Optimal Bellman equations:
According to the Bellman optimality principle: if a policy is optimal at state s, then from s+1 onward it must also be optimal. This leads to the following optimality equations:
- For the optimal state-value function:
$$
V^{*}(s) = \max_{a} \sum_{s', r} P(s', r | s, a) \left[ r + \gamma V^{*}(s') \right]
$$
- For the optimal action-value function:
$$
Q^{*}(s, a) = \sum_{s', r} P(s', r | s, a) \left[ r + \gamma \max_{a'} Q^{*}(s', a') \right]
$$

## Temporal Difference Prediction
Temporal Difference (TD) learning is a model-free reinforcement learning method that updates value estimates based on the difference between consecutive predictions. The TD(0) update rule for the state-value function is given by:
$$
V(S_t) \leftarrow V(S_t) + \alpha \left[ R_t + \gamma V(S_{t+1}) - V(S_t) \right]
$$
where \( \alpha \) is the learning rate.
$\alpha$: learning rate, \( 0 < \alpha \leq 1 \)
$\delta_t = R_t + \gamma V(S_{t+1}) - V(S_t)$: TD error

### On-policy vs Off-policy
- **On-policy methods**: Learn the value of the policy being carried out by the agent. Example: SARSA (State-Action-Reward-State-Action).
$$
Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha \left[ R_t + \gamma Q(S_{t+1}, A_{t+1}) - Q(S_t, A_t) \right]
$$

- **Off-policy methods**: Learn the value of the optimal policy independently of the agent's actions. Example: Q-learning.
$$
Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha \left[ R_t + \gamma \max_{a} Q(S_{t+1}, a) - Q(S_t, A_t) \right]
$$
