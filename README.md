# Parallel A* Search Algorithm

---

## Outline
1. A* Search Algorithm
2. Experimental Setup
3. Centralized Parallel A*
4. Analyzing CPA
5. Decentralized Parallel A*

---

## A* Search Algorithm
- **Informed Search Algorithm**: Utilizes heuristic information.
- **Best-First Search**: Evaluates nodes using the formula:
  \[
  f(n) = g(n) + h(n)
  \]
  - `g(n)`: Cost function, the actual cost from the start node to node `n`.
  - `h(n)`: Heuristic function, which should be admissible (never overestimates).
  - Example: In a shortest path problem, `h(n)` could be the straight-line distance.

---

## Experimental Setup
- **Graph/Map Construction**:
  - Data sourced from real road data in Hsinchu using OpenStreetMap.
- **Heuristic**:
  - The straight-line distance between each node and the target node.

---

## Centralized Parallel A*
### Data Structures
1. **Node Table**:
   - `ID`, `g`, `h`, `previous`, `OPEN`, `CLOSED`.
2. **Edge Table**:
   - `start`, `end`, `distance`.
3. **Locks**:
   - `Lock1`: OPEN/CLOSED list.
   - `Lock2`: Incumbent cost.

---

### Example of Centralized Parallel A*
- Threads process nodes in parallel using the shared OPEN/CLOSED lists.
- The algorithm maintains locks to ensure thread safety.

---

## Decentralized Parallel A*
- **Key Features**:
  - Each thread has its own `OPEN`, `CLOSED`, and `BUFFER` sets.
  - Faster than Centralized Parallel A*.
- **Constraint**:
  - The graph must not be bidirectional to prevent oscillation.

---

## Amdahl's Law Analysis
- **Speed-Up Achieved**: ~4.98x using 8 threads.
- **Parallelizable Proportion**: \( p = 0.91 \).
- Bottleneck: Searching the edges table to find neighbors.

---

## Optimizations
- **Indexing Solution**:
  - Introduce `nodeToNodeIdx` and `nodeToEdgeIdx` for efficient lookup.
- **Hardware Requirements**:
  - Minimum Intel i5 8257U (4 cores, 8 threads).

---

## References
1. Alex Fukunaga, Adi Botea, Yuu Jinnai, and Akihiro Kishimoto, “A Survey of Parallel A*.”
2. Ariana Weinstock and Rachel Holladay, “Parallel A* Graph Search.”

---
