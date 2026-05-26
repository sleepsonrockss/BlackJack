# OpenAI Gymnasium Blackjack RL Task
 
A reinforcement learning implementation for the classic card game Blackjack using OpenAI Gymnasium.
 
## Overview
 
The Blackjack environment from Gymnasium is a simple yet effective testbed for reinforcement learning algorithms. The goal is to train an agent to learn an optimal policy for playing Blackjack that maximizes expected winnings.
 
## Game Rules
 
- **Objective**: Get a hand value as close to 21 as possible without exceeding it
- **Card Values**: 
  - Number cards (2-10): Face value
  - Face cards (J, Q, K): 10
  - Aces: 1 or 11 (chosen to maximize hand value without busting)
- **Player Actions**:
  - `0`: Stand (stop taking cards)
  - `1`: Hit (take another card)
- **Winning Conditions**:
  - Player reaches 21 without busting: Win (+1)
  - Player doesn't bust while dealer does: Win (+1)
  - Both stand with player's hand > dealer's: Win (+1)
  - Tie (same hand value): Draw (0)
  - Player busts or dealer's hand > player's: Lose (-1)
## Environment Details
 
### State Space
The environment returns a 3-tuple state:
- **Player's current sum**: 4-31 (integer)
- **Dealer's showing card**: 2-11 (integer)
- **Usable ace**: Boolean (True if player has an ace counted as 11)
Total: 10 × 10 × 2 = 200 possible states
 
### Action Space
- **Action 0**: Stand
- **Action 1**: Hit
### Rewards
- **+1**: Win
- **0**: Draw
- **-1**: Lose

# Q-Learning
 
## Overview
 
Q-learning is a **model-free reinforcement learning algorithm** that learns the value of actions in states to find an optimal policy. It learns a function Q(s, a) that estimates the expected cumulative discounted reward of taking action `a` in state `s`.
 
## The Update Rule
 
The core update equation is:
 
```
Q(s, a) ← Q(s, a) + α [r + γ max_a' Q(s', a') - Q(s, a)]
```
 
Where:
- `α` is the learning rate
- `r` is the immediate reward
- `γ` is the discount factor (0 to 1)
- `s'` is the next state
- `max_a' Q(s', a')` is the maximum Q-value in the next state
The term `[r + γ max_a' Q(s', a') - Q(s, a)]` is the **temporal difference error**.
 
## Key Characteristics
 
- **Off-policy**: Learns the optimal policy while following an exploratory policy
- **Model-free**: No need for a model of environment dynamics
- **Convergence**: Guaranteed to converge to optimal Q-values under appropriate conditions
- **Discrete spaces**: Works best with discrete states and actions
## Exploration Strategy
 
Q-learning requires balancing exploration and exploitation. The most common approach is **ε-greedy**:
- With probability `ε`, choose a random action
- With probability `1 - ε`, choose the action with the highest Q-value
## Convergence
 
Q-learning converges to the optimal action-value function Q* if:
1. Every state-action pair is visited infinitely often
2. The learning rate α decreases appropriately
3. Rewards are bounded
From the optimal Q-values, the optimal policy is simply: **π*(s) = argmax_a Q(s, a)**
 
