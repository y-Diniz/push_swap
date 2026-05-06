# Push Swap

A sorting algorithm project developed as part of the 42 curriculum, focused on efficiency, algorithm design, and stack manipulation.

---

## 📊 Grade

96%

---

## About

**Push Swap** is a project where the goal is to sort a list of integers using two stacks and a limited set of operations.

* Stack **A** starts with unsorted integers
* Stack **B** starts empty
* The objective is to sort stack A in ascending order using the **fewest operations possible**

---

## Allowed Operations

### Swap

* `sa`, `sb`, `ss`

### Push

* `pa`, `pb`

### Rotate

* `ra`, `rb`, `rr`

### Reverse Rotate

* `rra`, `rrb`, `rrr`

---

## Algorithm Overview

This implementation follows a **3-step strategy**:

1. **Split stack A → B**
2. **Reinsert elements using cost-based optimization**
3. **Final alignment**

---

## 📥 Splitting Phase

All elements except the **3 largest** are pushed to stack B:

### 💡 Key Idea

* Elements are indexed from `0 → n-1`
* Only elements `< (n - 3)` go to stack B
* The 3 largest elements remain in A, then a small, optimal routine sorts the remaining elements.

---

## 🔁 Reinsertion Phase

* Compute cost for each element in B
* Execute the cheapest move
* Repeat until B is empty

---

### 📍 Target Position (stack A)

For each element in stack B:

* Find the smallest element in A that is greater than it
* This determines where it should be inserted

Costs calculated:

* `cost_ra` → rotations using `ra`
* `cost_rra` → rotations using `rra`

---

### 🔄 Rotation Cost (stack B)

For each element in stack B:

* `cost_rb` → rotations using `rb`
* `cost_rrb` → reverse rotations using `rrb`

---

### 💰 Total Cost Strategies

Four movement strategies are evaluated:

#### 🔁 1. Rotate both stacks (`rr`)

```c
rr = max(cost_ra, cost_rb);
```

#### 🔁 2. Reverse rotate both (`rrr`)

```c
rrr = max(cost_rra, cost_rrb);
```

#### 🔀 3. Rotate A + reverse rotate B

```c
ra_rrb = cost_ra + cost_rrb;
```

#### 🔀 4. Reverse rotate A + rotate B

```c
rra_rb = cost_rra + cost_rb;
```

---

### 🏆 Choosing the Best Move

```c
total_cost = min(rr, rrr, ra_rrb, rra_rb);
```

The algorithm selects the **lowest-cost strategy**.

---

### 🔍 Cheapest Element Selection

* Iterate through stack B
* Choose the node with the smallest `total_cost`

---

### Execution

Depending on the chosen strategy:

* Perform rotations (`rr`, `rrr`, or mixed)
* Push element to stack A

---

## Final Alignment

* Rotates stack A until the **smallest element is at the top**
* Ensures the stack is fully sorted

---

## 🔄 Full Execution Flow

```text
Unsorted A
   ↓
Push all except 3 → B
   ↓
Sort 3 elements in A
   ↓
Compute costs
   ↓
Move cheapest element
   ↓
Repeat until B is empty
   ↓
Final rotation
   ↓
Sorted A
```

---

## Compilation

```bash
make
```

---

## Usage

```bash
./push_swap 4 67 3 87 23
```

---

### Checker

```bash
./push_swap 4 67 3 87 23 | ./checker 4 67 3 87 23
```

Output:

* `OK` → sorted
* `KO` → incorrect

---

## Performance

* Small inputs → optimized manual sorting
* Large inputs → split + cost-based reinsertion
* Focus on minimizing total operations

---

## Concepts Covered

* Sorting algorithms
* Stack manipulation
* Greedy algorithms
* Cost analysis
* Optimization strategies

---

## Notes

* Uses indexed values for efficient comparisons
* Compiled with: `-Wall -Wextra -Werror`
* No external libraries
* Emphasis on performance and operation count

---
