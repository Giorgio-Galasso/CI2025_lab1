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

## ⚙️ Problem Setup

### Parameters
Each problem instance defines:
- `NUM_KNAPSACKS`: number of knapsacks  
- `NUM_ITEMS`: number of available items  
- `NUM_DIMENSIONS`: number of constraints (e.g., weight, volume, cost, etc.)  
- `VALUES`: array of item values  
- `WEIGHTS`: matrix of resource consumption per item and per dimension  
- `CONSTRAINTS`: maximum capacity allowed for each dimension  

Example initialization:

```python
rng = np.random.default_rng(seed=42)
NUM_KNAPSACKS = 3
NUM_ITEMS = 20
NUM_DIMENSIONS = 2

VALUES = rng.integers(0, 100, size=NUM_ITEMS)
WEIGHTS = rng.integers(0, 100, size=(NUM_ITEMS, NUM_DIMENSIONS))
CONSTRAINTS = rng.integers(0, 100 * NUM_ITEMS // NUM_KNAPSACKS, size=NUM_DIMENSIONS)

Larger problems (Problem 2 and 3) use the same structure but scale the parameters up to 100 knapsacks and 5000 items.

🧩 Algorithm Description
Random Mutation Hill Climbing (RMHC)

The RMHC algorithm starts with an initial random solution and iteratively modifies it through random mutations.
If the new configuration produces a higher fitness (better total value while respecting constraints), it replaces the current solution.

Pseudocode
Initialize random solution S for all knapsacks
Evaluate f(S)
Repeat until MAX_STEPS:
    Generate S' by flipping one or more bits of S (tweak)
    Evaluate f(S')
    If f(S') > f(S):
        S ← S'
Return best solution found
🧮 Implementation Details
🔹 Fitness Evaluation

Each knapsack is evaluated using the function:

def evaluate(knapsack):
    if all(np.sum(WEIGHTS[knapsack], axis=0) < CONSTRAINTS):
        return np.sum(VALUES[knapsack])
    else:
        return -1


If the total weight in every dimension is below the constraint limit, the fitness equals the sum of item values.

Otherwise, an infeasible configuration is penalized with -1.

🔹 Mutation Operator

The tweak() function randomly flips one or more bits of the current solution, introducing new candidate configurations:

def tweak(knapsack, items_taken):
    new_knapsack = knapsack.copy()
    index = None
    while index is None or np.random.random() < 0.4:
        index = np.random.randint(0, NUM_ITEMS)
        if items_taken[index] == True:
            index = None
        else:
            new_knapsack[index] = not new_knapsack[index]
    return new_knapsack


This process ensures diversity and prevents multiple knapsacks from taking the same item (items_taken mask).

🔁 Optimization Loop

The main loop executes the RMHC process for each knapsack:

solution = np.full((NUM_KNAPSACKS, NUM_ITEMS), False)
items_taken = np.full(NUM_ITEMS, False)

for knapsack_id in range(NUM_KNAPSACKS):
    knapsack = solution[knapsack_id]
    best_solution = knapsack
    history = [evaluate(best_solution)]

    for n in range(MAX_STEPS):
        new_solution = tweak(best_solution, items_taken)
        history.append(evaluate(new_solution))
        if evaluate(new_solution) > evaluate(best_solution):
            best_solution = new_solution

    items_taken = items_taken + best_solution
    solution[knapsack_id] = best_solution


Each knapsack is optimized independently while respecting global item usage.

📊 Final Evaluation

After optimization, the total value and the total weights per knapsack are computed:

total_value = 0
total_weights = np.zeros((NUM_KNAPSACKS, WEIGHTS.shape[1]))

for knapsack_id in range(NUM_KNAPSACKS):
    total_value += np.sum(VALUES[solution[knapsack_id]], axis=0)
    total_weights[knapsack_id] = np.sum(WEIGHTS[solution[knapsack_id]], axis=0)

print(total_value)

🧠 Observations

The algorithm effectively handles multi-dimensional and multi-knapsack constraints.

It converges toward high-quality feasible solutions, though it may get stuck in local optima.

Increasing the number of iterations (MAX_STEPS) generally improves solution quality but also increases computation time.

🚀 Possible Improvements

Introduce adaptive mutation rates to balance exploration and exploitation.

Add restart strategies to escape local optima.

Implement parallel RMHC to optimize multiple knapsacks simultaneously.

Compare performance with Simulated Annealing or Genetic Algorithms.

🧾 Author

[Giorgio Galasso]
Computational Intelligence — Laboratory 1
Academic Year: 2025/2026