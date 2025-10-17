# 🧠 Lab 1 — Computational Intelligence  
## Random Mutation Hill Climbing for the Multi-Dimensional Multi-Knapsack Problem

---

## 📘 Introduction

This laboratory aims to apply the **Random Mutation Hill Climbing (RMHC)** algorithm to solve the **0-1 Multi-Dimensional Multi-Knapsack Problem (MDMKP)**.  
The task consists in selecting a subset of items to be placed into several independent knapsacks so that the **total value is maximized** while respecting **multiple capacity constraints** across all dimensions.

The knapsack problem is a well-known **NP-hard combinatorial optimization** challenge.  
Its multidimensional and multi-knapsack extension increases complexity, making heuristic or metaheuristic methods like RMHC suitable for approximating optimal solutions.

The RMHC algorithm explores the solution space through **random local mutations** and **greedy acceptance** of improved solutions, demonstrating the balance between *exploration* and *exploitation* typical of stochastic search methods.

---

## 💡 Inspiration

This implementation was **inspired by previous academic lab exercises** and examples from **earlier academic years** of the *Computational Intelligence* course.  
The structure and core logic of the algorithm were reinterpreted, extended, and adapted to handle the **multi-dimensional and multi-knapsack** formulation, while maintaining the conceptual foundation of Random Mutation Hill Climbing.  

The code was entirely reimplemented, with additional improvements in readability, modularity, and scalability, while preserving the heuristic approach introduced in earlier course materials.

---

## ⚙️ Problem Setup

### Parameters
Each problem instance defines:
- `NUM_KNAPSACKS`: number of knapsacks  
- `NUM_ITEMS`: number of available items  
- `NUM_DIMENSIONS`: number of constraints (e.g., weight, volume, cost, etc.)  
- `VALUES`: array of item values  
- `WEIGHTS`: matrix of resource consumption per item and per dimension  
- `CONSTRAINTS`: maximum capacity allowed for each dimension  

🧩 Algorithm Description
Random Mutation Hill Climbing (RMHC)

The RMHC algorithm starts with an initial random solution and iteratively modifies it through random mutations.
If the new configuration produces a higher fitness (better total value while respecting constraints), it replaces the current solution.

🧮 Implementation Details
🔹 Fitness Evaluation

Each knapsack is evaluated using a function such that if the total weight in every dimension is below the constraint limit, the fitness equals the sum of item values.

Otherwise, an infeasible configuration is penalized with -1.

🔹 Mutation Operator

The tweak function randomly flips one or more bits of the current solution, introducing new candidate configurations.

This process ensures diversity and prevents multiple knapsacks from taking the same item (items_taken mask).

🔁 Optimization Loop

The main loop executes the RMHC process for each knapsack.

Each knapsack is optimized independently while respecting global item usage.

📊 Final Evaluation

After optimization, the total value and the total weights per knapsack are computed some useful metrics.

🚀 Possible Improvements

Introduce adaptive mutation rates to balance exploration and exploitation.

Add restart strategies to escape local optima.

Implement parallel RMHC to optimize multiple knapsacks simultaneously.

Compare performance with Simulated Annealing or Genetic Algorithms.

🧾 Author

Giorgio Galasso

Computational Intelligence — Laboratory 1
Academic Year: 2025/2026