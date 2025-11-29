# Summary of Key Concepts: Search and Problem-Solving in AI

This summary includes **all important concepts** from the text, each clearly explained.

---

# 1. Search and Problem-Solving in AI
Many AI tasks can be expressed as **search problems**.  
To solve them, an AI system must:
- define the problem correctly,
- construct an appropriate search space,
- choose an effective search algorithm.

This process is a core AI skill.

---

# 2. Basic Search Algorithms (Prerequisites)
AI search relies on foundational traversal algorithms:
- **Breadth-First Search (BFS)** – explores all nodes layer by layer; finds the shortest path in unweighted graphs.
- **Depth-First Search (DFS)** – explores one branch deeply before backtracking; uses little memory but may get stuck.
- **Best-First Search** – uses a heuristic to explore promising nodes first.
- **A\*** – a special case of best-first search; combines cost so far (*g*) and heuristic estimate (*h*). Finds optimal solutions when the heuristic is admissible.

These algorithms are essential for solving structured search problems.

---

# 3. Formulating Problems as Search
To use search effectively, the problem must be expressed in a formal structure.

## 3.1 Search Space
**Search space** = all allowed states of the problem.  
Each state represents one configuration of the system.

## 3.2 Transitions
**Transitions** = allowed moves between states.  
Defined by rules of the system (e.g., legal moves in a puzzle or navigation network).

## 3.3 Costs
Some transitions have **costs**, which represent:
- distance,
- time,
- resources,
- or any metric relevant to the problem.

These costs influence the choice of algorithm (e.g., A\* is used when costs vary).

---

# 4. State Transition Diagram
A **state transition diagram** is a graph where:
- nodes = states,
- edges = transitions between states.

It visualizes the entire search space.

**Purpose:**  
- Helps understand all possible actions,
- Shows structure of the problem,
- Supports the application of search algorithms.

---

# 5. Example: Wolf–Goat–Cabbage Puzzle
The text uses a classic puzzle to illustrate search concepts.

## 5.1 Puzzle Setup
A farmer must move:
- a wolf (w),
- a goat (g),
- a cabbage (c)

across a river in a boat that can carry only **one item at a time**.

Rules:
- Wolf cannot be left alone with the goat.
- Goat cannot be left alone with the cabbage.


[Graph theory: Wolf, sheep, cabbage](https://www.youtube.com/watch?v=pBT-8gqhHzo)

## 5.2 Representing States
A state describes which riverbank contains each entity, e.g.:

`c|fwg`  
Left bank: cabbage  
Right bank: farmer, wolf, goat

Initial state:  
`fwgc|`

Goal state:  
`|fwgc`

## 5.3 Constructing the State Transition Diagram
- Each valid configuration = a node.  
- Each legal move (farmer crossing with/without cargo) = an edge.  
- Only 10 valid states exist.

Building the diagram makes the solution trivial for an algorithm.

**Key lesson:**  
Formulating the search space transforms a seemingly intelligent puzzle into a routine computational problem.

---

# 6. Why This Approach Matters
Although constructing diagrams for small puzzles is tedious, search techniques become essential in **large-scale problems** where:
- humans cannot explore all possibilities,
- systematic algorithms outperform intuition.

Examples include:
- route planning,
- robotics,
- game AI,
- logistics and scheduling,
- planning under uncertainty.

**Key idea:**  
Search + formal representation = scalable problem-solving power.

---

# Final Key Insight
AI search is powerful not because it imitates human reasoning, but because it **systematically explores** all possible states in a defined space—something humans cannot do efficiently at scale.


# Summary of Key Concepts: Breadth-First Search (BFS) and Depth-First Search (DFS)

This summary includes **all the important concepts** from the text, each explained clearly and concisely in MD format.

---

# 1. Generic Search Algorithm Template

Many search algorithms share the same structure. The pseudo-code below represents a **general template**:

search(start_node):
node_list = list() # queue, stack, or other list structure
visited = set() # tracks visited nodes
add start_node to node_list

````c#
while node_list not empty:
    node = node_list.first()   # take next node based on data structure
    remove node from node_list

    if node not in visited:
        visited.add(node)

        if goal_node(node):
            return node        # goal found

        add node.neighbors() to node_list
return None

```` 


### **Key Idea**
The **choice of data structure** used for `node_list` determines the search strategy:
- Queue → BFS
- Stack → DFS

Everything else stays the same.

---

# 2. Node List Operations and Data Structures

## **2.1 Breadth-First Search (BFS)**
Uses a **queue** (FIFO = First In, First Out).

- **enqueue** = add node to back of the queue  
- **dequeue** = remove node from front of the queue  

### **BFS Behavior**
- Explores neighbors **level by level**.
- Expands all nodes at distance *d* before exploring nodes at distance *d+1*.
- Works like a “wave” expanding outward from the start node.

### **Guarantees**
- **Always finds the shortest path** in terms of number of transitions (when all edges have equal cost).

---

## **2.2 Depth-First Search (DFS)**
Uses a **stack** (LIFO = Last In, First Out).

- **push** = add node to top of the stack  
- **pop** = remove the most recently added node  

### **DFS Behavior**
- Explores **one path deeply** before backtracking.
- Goes as far as possible along one branch, then returns.

### **DFS Characteristics**
- Does **not** guarantee the shortest path.
- Uses **less memory** than BFS.
- Can get stuck exploring deep or infinite branches if not controlled.

---

# 3. The Role of goal_node
`goal_node(node)` checks whether the current node is the goal.

Possible situations:
- **Goal-directed search** (e.g., find a path to a target node):
  - `goal_node(node)` returns True only at the destination.
- **Full traversal** (no specific goal):
  - `goal_node(node)` always returns False.

---

# 4. Recursive vs. Iterative DFS

Many students learn **recursive DFS**, which seems different but is actually identical in behavior.

### Why?
- The **call stack** in recursion functions exactly like the **explicit stack** in the iterative version.
- Every recursive call pushes a new state onto the stack.
- When a recursive call returns, it pops that state.

### Key Insight
**Recursive DFS = DFS using an implicit stack.**

---

# 5. Why BFS Finds the Shortest Path

BFS expands the search in **layers**:

1. First explores all nodes at distance 1  
2. Then all nodes at distance 2  
3. Then distance 3, etc.

If a goal exists at the shortest distance `k`, BFS will reach it **before** exploring any deeper paths.  
Thus, BFS **guarantees minimal number of steps**.

---

# 6. Why DFS Does *Not* Guarantee the Shortest Path

DFS may:
- follow a long, deep path before reaching a shorter alternative
- explore irrelevant branches first
- get lost in depth

DFS prioritizes **depth**, not optimality.

---

# 7. When DFS Is Better Than BFS

DFS is preferred when:
- The search space is very large but **solutions are deep**.
- You don’t need the shortest solution.
- Memory is limited (DFS needs almost no extra memory).
- You want to reach a goal quickly by “guessing” promising paths.
- The problem has **few valid paths** but each is long.

### Example: Sudoku
DFS is better because:
- Sudoku puzzles involve deep reasoning with many choices at each step.
- BFS would require massive memory (branching is huge).
- DFS can follow a sequence of moves until it reaches a contradiction and backtrack.

**Key Idea:**  
DFS is suited to **constraint satisfaction problems** like Sudoku, where you explore one possibility deeply before trying another.

---

# Final Summary Table

| Concept | BFS | DFS |
|--------|-----|-----|
| Data structure | Queue (FIFO) | Stack (LIFO) |
| Nature | Layer-by-layer | Depth-first, branch-first |
| Shortest path? | ✔ Yes | ✘ No |
| Memory use | High | Low |
| Best for | Finding shortest path, shallow solutions | Deep solutions, constraint problems |
| Risk | Large memory use | Getting lost in deep paths |
| Equivalent recursive form? | Not common | Recursive DFS = implicit stack |

---


# Summary of Key Concepts: Informed Search and A*

This summary includes **all important concepts** from the text, each clearly explained in MD code format.

---

# 1. Why We Need Informed Search
Some search problems involve **different costs for different transitions**.  
Examples:
- Travel time between locations varies.
- Some actions take longer than others.
- Distances between nodes differ.

Because of varying costs:
- Simply counting number of transitions (as in BFS) is not enough.
- We need algorithms that can handle **weighted edges** and **cost differences**.

---

# 2. Best-First Search
Best-first search selects the **next node** based on a criterion that ranks nodes.

### Key Idea
Choose the most promising node first, rather than expanding blindly.

### Data Structure
Uses a **priority queue** instead of:
- a queue (BFS), or
- a stack (DFS).

Nodes in the priority queue are ordered by a numerical value (cost or heuristic).

---

# 3. Dijkstra’s Algorithm
A special case of best-first search.

### Definition
Dijkstra’s algorithm always expands the node with the **smallest accumulated path cost** from the start.

### Properties
- Guarantees finding the **lowest-cost path** when all edge costs are non-negative.
- If all transitions cost the same, Dijkstra = BFS.

### Why it works
It always explores paths in order of increasing cost, ensuring optimality.

---

# 4. Modification to the Generic Search Template
In informed search (including Dijkstra and A*):
- **We do not check whether a node has been visited before.**

### Why?
A “visited” node might later be found through a **cheaper path**.  
Skipping the visited check ensures:
- all cheaper paths are examined,
- optimality is preserved.

This differs from BFS/DFS, where revisiting is unnecessary or harmful.

---

# 5. Priority Queue in Informed Search
The priority queue orders nodes by:
- path cost (Dijkstra),
- heuristic value,
- or a combination of both (A*).

Can be:
- **min-priority queue** (expand smallest value first),
- **max-priority queue** (expand largest value first),
depending on the task.

---

# 6. The Problem With Uninformed Search
Methods like BFS or Dijkstra expand in **all directions equally**.  
They:
- do not consider the location of the goal,
- waste time exploring irrelevant nodes,
- behave symmetrically.

### Example
When searching a map, BFS explores north, south, east, and west uniformly, even if the goal is far to the east.

---

# 7. Informed Search
Informed search uses **additional knowledge**—a *heuristic*—to guide the search more efficiently.

## Heuristic (h(node))
A heuristic is an **estimate of the cost** from a node to the goal.

Examples:
- straight-line (Euclidean) distance,
- Manhattan distance on a grid,
- estimated remaining steps.

### Purpose
Helps prioritize nodes that **appear closer** to the goal.

---

# 8. The Problem With Greedy Heuristic Search
A purely heuristic-based search (greedy best-first) expands nodes based only on `h(node)`.

### Issue
It might:
- chase nodes that *look* promising,
- ignore the actual cost so far,
- find non-optimal paths,
- get stuck in misleading directions.

Thus, we need a balance between:
- actual cost (what we already paid),
- estimated remaining cost (how far to go).

---

# 9. A* Search (A-Star)
A* combines:
- **cost so far** (g)
- **estimated remaining cost** (h)

using the function:

`f(node) = cost_so_far(node) + h(node)`


### Components
- **cost_so_far (g)**: real cost from start to the current node.
- **heuristic (h)**: estimated cost from current node to goal.
- **total (f)**: estimated total cost of the full path.

### Behavior
A* always expands the node with the lowest **f-value**.

---

# 10. Why A* Is Powerful
A* is:
- **goal-directed** (thanks to heuristic),
- **cost-aware** (thanks to accumulated cost),
- **optimal** (if the heuristic is admissible),
- dramatically more efficient than BFS, DFS, or Dijkstra.

### Intuition
A* reaches the goal sooner because it:
- moves *toward* the goal using the heuristic,
- avoids bad paths using cost information.

---

# 11. Summary of Key Concepts

| Concept | Meaning | Why It Matters |
|--------|---------|----------------|
| **Best-first search** | Expand most promising node | More efficient than blind search |
| **Dijkstra’s algorithm** | Expand node with smallest cost | Finds optimal lowest-cost path |
| **Priority queue** | Orders nodes by value | Used in all informed search |
| **Heuristic** | Estimate of distance to goal | Guides search toward goal |
| **Greedy search** | Uses only heuristic | Fast but not optimal |
| **A\*** | Uses both cost + heuristic | Fast **and** optimal |
| **f = g + h** | A* evaluation function | Balances cost and goal direction |

---

# 12. Final Note
Informed search is a major upgrade over basic search algorithms.  
A* in particular is one of the **most important algorithms in AI**, used in:
- navigation,
- robotics,
- games,
- routing,
- planning.

