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
## Installation
 
### Requirements
- Python 3.7+
- gymnasium
- numpy
- matplotlib (optional, for visualization)
