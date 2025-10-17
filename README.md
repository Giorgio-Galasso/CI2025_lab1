# 🧠 Lab 1 — Computational Intelligence  
## Introduction

The first laboratory of the *Computational Intelligence* course focuses on applying the **Random Mutation Hill Climbing (RMHC)** algorithm to solve the **0-1 Knapsack Problem** in its **multi-dimensional and multi-knapsack** formulation.

The Knapsack Problem is a classic **combinatorial optimization** problem in which, given a set of items—each with an associated value and one or more constraints (such as weight, volume, or cost)—the goal is to select the combination of items that **maximizes the total value** without exceeding the **capacity limits**.

In the **multi-dimensional version**, each item is characterized by multiple resource constraints (one per dimension), while in the **multi-knapsack version**, the solution must distribute items among **multiple independent knapsacks**, each with its own set of limitations.  
This makes the problem **NP-hard**, meaning that exact optimization methods become computationally infeasible as the problem size grows.

The **RMHC** algorithm belongs to the family of **stochastic metaheuristics** and is based on a **local search** process: starting from a randomly generated solution, the algorithm introduces **random mutations** (bit flips) and accepts the new configuration only if it **improves the objective function**.  
Despite its simplicity, RMHC provides an effective baseline for understanding iterative optimization and the trade-off between **exploration and exploitation**.

In this laboratory, the problem is formalized and implemented in **Python**, using **NumPy** for efficient data manipulation and vectorized computations.
