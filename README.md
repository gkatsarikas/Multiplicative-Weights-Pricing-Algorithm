# Multiplicative Weights Pricing Algorithm

This repository contains a simulation of a pricing strategy using the Multiplicative Weights (MW) algorithm under two user behavior scenarios: naive and smart.

## Overview

The algorithm selects among five pricing options for a service. The options are computed as:
- \(p_0 = a^2 \times P\)
- \(p_1 = a \times P\)
- \(p_2 = P\)
- \(p_3 = b \times P\)
- \(p_4 = b^2 \times P\)

where:
- \(a = 0.5\)
- \(b = 1.5\)
- \(P\) is a base price drawn uniformly from the interval \([1.5, 2.5]\).

## User Scenarios

### Naive User
- **Behavior:** The user chooses between our service and a competitor with equal probability (50/50), regardless of the prices shown.
- **Outcome:** The MW algorithm learns to favor the highest price option since a high price directly translates into a high reward when chosen.

### Smart User
- **Behavior:** For the first 25% of rounds, the user behaves like a naive user. After that, the user compares prices between our service and the competitor (whose price is randomly drawn from \([0,4]\)) and selects the lower price.
- **Outcome:** The algorithm initially favors high prices but then adapts by shifting to lower prices in order to win the sale, resulting in a lower cumulative profit.

## How the Algorithm Works

The algorithm uses a bandit version of the Multiplicative Weights update rule with the following key steps:
1. **Initialization:** Each pricing option starts with an equal weight.
2. **Action Selection:** At each round, an action (pricing option) is chosen with probability proportional to its weight.
3. **Feedback & Reward:** Based on user behavior (naive or smart), a reward equal to the chosen price (if the sale occurs) is received.
