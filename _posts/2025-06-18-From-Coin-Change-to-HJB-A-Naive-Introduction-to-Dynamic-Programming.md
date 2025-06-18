---
title: "From Coin Change to HJB: A Naive Introduction to Dynamic Programming"
date: 2025-06-18
layout: cool-post
---

## Table of Contents

- [1. A Naive Example of Dynamic Programming: Minimum Coin Change Problem](#1-a-naive-example-of-dynamic-programming-minimum-coin-change-problem)
  - [1.1 Problem Statement](#11-problem-statement)
  - [1.2 What is Dynamic Programming?](#12-what-is-dynamic-programming)
  - [1.3 Approach](#13-approach)
  - [1.4 Step-by-step Computation](#14-step-by-step-computation)
  - [1.5 Final DP Table](#15-final-dp-table)
  - [1.6 Conclusion](#16-conclusion)
- [2. From Inventory Problem to HJB via Dynamic Programming Principle](#2-from-inventory-problem-to-hjb-via-dynamic-programming-principle)
  - [2.1 Problem Setting: Optimal Inventory Liquidation](#21-problem-setting-optimal-inventory-liquidation)
  - [2.2 Discrete-Time Dynamic Programming](#22-discrete-time-dynamic-programming)
  - [2.3 Transition to Continuous Time](#23-transition-to-continuous-time)
  - [2.4 HJB Equation from Instantaneous Cost](#24-hjb-equation-from-instantaneous-cost)
  - [2.5 Intuition Recap](#25-intuition-recap)
  - [2.6 Analogy Table](#26-analogy-table)
  - [2.7 Conclusion](#27-conclusion)

## 1. A Naive Example of Dynamic Programming: Minimum Coin Change Problem

### 🧮1.1 Problem Statement

Suppose you are given coins of denominations `{1, 3, 4}`, and you want to make a total amount of 6 using the **minimum number of coins**. This is a classic example where dynamic programming is very useful.

### 🧮1.2 What is Dynamic Programming?

Dynamic Programming (DP) is a method used to solve problems by:

1. Breaking the problem into smaller subproblems.
2. Storing the solutions to those subproblems.
3. Building up the solution to the full problem using those stored values.

### 🧮1.3 Approach

Let \\( dp[i] \\) represent the minimum number of coins needed to make amount \\( i \\). Our goal is to compute \\( dp[6] \\).

We initialize: \\( dp = [0, ∞, ∞, ∞, ∞, ∞, ∞] \\).

Here, \\( dp[0] = 0 \\) because 0 coins are needed to make amount 0. All other values are initially set to infinity to represent that they are not yet computed.

### 🧮1.4 Step-by-step Computation

We compute \\( dp[i] \\) for \\( i = 1 \\) to \\( 6 \\) by trying each coin and selecting the one that gives the minimum total coins.

- **dp[1]**:
  - Using coin 1: \\( dp[0] + 1 = 1 \\)
  - Coins 3 and 4 are too large.
  - → \\( dp[1] = 1 \\)

- **dp[2]**:
  - Using coin 1: \\( dp[1] + 1 = 2 \\)
  - Coins 3 and 4 are too large.
  - → \\( dp[2] = 2 \\)

- **dp[3]**:
  - Coin 1: \\( dp[2] + 1 = 3 \\)
  - Coin 3: \\( dp[0] + 1 = 1 \\)
  - Coin 4 is too large.
  - → \\( dp[3] = 1 \\)

- **dp[4]**:
  - Coin 1: \\( dp[3] + 1 = 2 \\)
  - Coin 3: \\( dp[1] + 1 = 2 \\)
  - Coin 4: \\( dp[0] + 1 = 1 \\)
  - → \\( dp[4] = 1 \\)

- **dp[5]**:
  - Coin 1: \\( dp[4] + 1 = 2 \\)
  - Coin 3: \\( dp[2] + 1 = 3 \\)
  - Coin 4: \\( dp[1] + 1 = 2 \\)
  - → \\( dp[5] = 2 \\)

- **dp[6]**:
  - Coin 1: \\( dp[5] + 1 = 3 \\)
  - Coin 3: \\( dp[3] + 1 = 2 \\)
  - Coin 4: \\( dp[2] + 1 = 3 \\)
  - → \\( dp[6] = 2 \\)

### 🧮1.5 Final DP Table

| Amount | dp[i] | Explanation   |
|--------|-------|---------------|
| 0      | 0     | Base case     |
| 1      | 1     | 1             |
| 2      | 2     | 1 + 1         |
| 3      | 1     | 3             |
| 4      | 1     | 4             |
| 5      | 2     | 4 + 1         |
| 6      | 2     | 3 + 3         |

### 🧮1.6 Conclusion

Dynamic Programming works well for this problem because:

- The problem has **overlapping subproblems**, e.g. computing \\( dp[4] \\) uses \\( dp[0], dp[1], dp[3] \\), which are reused later.
- It has an **optimal substructure** — the optimal solution to a problem includes the optimal solution to its subproblems.

By solving smaller problems first and storing their results, we avoid recomputation and solve the overall problem efficiently.

---

## 2. From Inventory Problem to HJB via Dynamic Programming Principle

### 🧮2.1 Problem Setting: Optimal Inventory Liquidation

Suppose you are a trader who holds an initial inventory of \\( q_0 = 10 \\) units and wants to sell all of it over a time interval \\([0, T]\\), say in 10 time steps. Each time you sell, your trades impact the price negatively (market impact), so you want to minimize the total expected cost of liquidation.

Your decision at each moment is the trading rate \\( v_t \\), i.e., how fast to sell. The goal is to find the optimal trading schedule that minimizes total cost.

### 🧮2.2 Discrete-Time Dynamic Programming

Define:

- \\( q_t \\): inventory at time \\( t \\)
- \\( v_t \\): trading rate (units sold per time step)
- \\( C_t(q) \\): minimal expected cost from time \\( t \\) onward, starting with inventory \\( q \\)

The Bellman equation is:

$$
C_t(q) = \min_{v} \left( \text{ImmediateCost}(q, v) + C_{t+1}(q - v) \right)
$$

This is the **Dynamic Programming Principle (DPP)**:

> The value function at time \\( t \\) is the best you can do now (min over controls), plus the value from future states.

### 🧮2.3 Transition to Continuous Time

Now we let time become continuous:

- \\( t \in [0, T] \\)
- Inventory becomes \\( q(t) \\)
- Control becomes trading rate \\( v(t) = -\dot{q}(t) \\)

Let \\( V(t, q) \\) be the value function: the minimal expected cost from time \\( t \\) onward, starting with inventory \\( q \\).

The DPP in continuous time becomes:

$$
V(t, q) = \min_v \left( \text{cost over } \Delta t + V(t + \Delta t, q - v \Delta t) \right)
$$

Using Taylor expansion:

\\[
V(t + \Delta t, q - v \Delta t) \approx V(t, q) + \partial_t V \cdot \Delta t - v \partial_q V \cdot \Delta t
\\]

Substituting:

$$
0 = \min_v \left( \text{InstantaneousCost}(q, v) + \partial_t V - v \partial_q V \right)
$$

### 🧮2.4 HJB Equation from Instantaneous Cost

Assume the cost of trading is quadratic in rate due to market impact:

\\[
\text{Instantaneous cost} = \frac{1}{2} \eta v^2
\\]

Then the HJB equation becomes:

$$
\partial_t V(t, q) + \min_v \left( \frac{1}{2} \eta v^2 - v \partial_q V(t, q) \right) = 0
$$

This is the **Hamilton–Jacobi–Bellman (HJB) equation**, derived directly from the continuous-time DPP.

### 🧮2.5 Intuition Recap

- Like in the coin example, we want to minimize total cost by solving from the end backwards.
- In discrete time: \\( V(t) = \min_v \{ \text{cost now} + V(t+1) \} \\)
- In continuous time: \\( \partial_t V \\) balances instantaneous cost and continuation value.
- The HJB equation is the limiting form of Bellman’s equation as \\( \Delta t \to 0 \\).

### 🧮2.6 Analogy Table

| Concept            | Coin Example                     | Inventory Example                                       |
|--------------------|----------------------------------|--------------------------------------------------------|
| State              | Amount left                      | Inventory \\( q \\), time \\( t \\)                     |
| Control            | Which coin to use                | Trading rate \\( v \\)                                 |
| Cost               | Number of coins                  | Trading cost, e.g., \\( \frac{1}{2} \eta v^2 \\)       |
| Value function     | Minimum coins to make amount     | Minimum expected trading cost \\( V(t, q) \\)          |
| Bellman equation   | \\( dp[i] = \min (1 + dp[i - c]) \\) | \\( V(t) = \min_v \{ \text{cost} + V(t + \Delta t) \} \\) |
| HJB equation       | --                               | \\( \partial_t V + \min_v \{ \text{cost} - v \partial_q V \} = 0 \\) |

### 🧮2.7 Conclusion

This shows that the HJB equation is nothing more than a continuous-time version of the recursive optimization used in dynamic programming. By solving the problem backwards and updating based on optimal local decisions, we arrive at a PDE that characterizes the value function.
